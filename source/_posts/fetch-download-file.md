---
title: fetch download file
date: 2019-09-20 02:35:30
tags:
  - js
  - java
---

fetch 下载文件

<!--more-->

> 设置头

```
UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
CorsConfiguration config = new CorsConfiguration();
config.setAllowCredentials(true);
config.addAllowedOrigin("*");
config.addAllowedHeader("*");
config.addAllowedMethod("*");
config.addExposedHeader("Content-Disposition");// 前端可获取头
config.setMaxAge(1800l);
source.registerCorsConfiguration("/**", config);
FilterRegistrationBean bean = new FilterRegistrationBean(new CorsFilter(source));
bean.setOrder(0);
return bean;
```

> java 代码

```
package org.demo.controller;

import java.io.FileOutputStream;
import java.io.OutputStream;

import javax.servlet.http.HttpServletResponse;

import org.apache.poi.hssf.usermodel.HSSFWorkbook;
import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Workbook;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping(value = "api/download")
public class DownloadController {

	@RequestMapping(value = "file", method = { RequestMethod.POST, RequestMethod.GET })
	@ResponseBody
	public void download(HttpServletResponse response) {

		response.setHeader("content-type", "application/octet-stream");
		response.setContentType("application/octet-stream");
//        response.setHeader("Content-Disposition", "attachment;filename=test123.xls");
		response.setHeader("Content-Disposition", "test123.xls");

		Workbook wb = new HSSFWorkbook();
		Sheet sheet = wb.createSheet("new sheet");
		Sheet sheet2 = wb.createSheet("second sheet");
		Row row = sheet.createRow(0);
		// Create a cell and put a value in it.
		Cell cell = row.createCell(0);
		cell.setCellValue(1);

		// Or do it on one line.
		row.createCell(1).setCellValue(1.2);
		row.createCell(3).setCellValue(true);
		try (OutputStream fileOut = new FileOutputStream("workbook.xls")) {
			wb.write(fileOut);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

		try (OutputStream out = response.getOutputStream()) {
			wb.write(out);
			out.flush();
		} catch (Exception e) {
			e.printStackTrace();
		}

	}
}
```

> html fetch

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>download</title>
  </head>
  <body>
    <button>Download</button>
  </body>
  <script>
    document.querySelector("button").addEventListener("click", () => {
      fetch("http://localhost:8889/api/download/file")
        .then(response => {
          const blob = response.blob();
          const filename = response.headers.get("Content-Disposition");
          console.log(filename);
          return {
            blob,
            filename
          };
        })
        .then(({ blob, filename }) => {
          blob.then(data => {
            // chrome
            const url = window.URL.createObjectURL(data);
            let link = document.createElement("a");
            link.setAttribute("href", url);
            // link.setAttribute("download", filename.split("=")[1]);
            link.setAttribute("download", filename);
            link.click();
          });
        });
    });
  </script>
</html>

```
