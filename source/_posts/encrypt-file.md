title: encrypt file
date: 2016-01-19 15:22:51
tags:
- java
---
encrypt file 
<!--more-->

~~~java
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.OutputStream;
import java.security.Key;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

import javax.crypto.Cipher;
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.DESedeKeySpec;
import javax.crypto.spec.IvParameterSpec;

import org.apache.commons.codec.binary.Base64;
import org.apache.commons.codec.binary.Hex;

/**
 *
 * @author Jay
 * @date   Jan 18, 2016
 *
 */
public class Encrypt {

	 private static byte keyiv[] = "12345678".getBytes();
	
	/**
	 * generate key
	 * @param str	
	 * @return
	 */
	public static String generateKeyByMd5(String str) {
		String result = "";
		try {
			MessageDigest messageDigest = MessageDigest.getInstance("md5");
			byte[] md5Bytes = messageDigest.digest(str.getBytes());
			result = Hex.encodeHexString(md5Bytes);
		} catch (NoSuchAlgorithmException e) {
			e.printStackTrace();
		}
		return result;
	}
	 
	/**
	 * 3des encrypt
	 * @param str
	 * @param key
	 * @return
	 */
	public static String encrypt3Des(String str, String key) {
		String returnStr = "";
		try {
			// key转换
			DESedeKeySpec deSedeKeySpec = new DESedeKeySpec(key.getBytes());
			SecretKeyFactory factory = SecretKeyFactory.getInstance("DESede");
			Key convertSecretKey = factory.generateSecret(deSedeKeySpec);
			// 加密
			Cipher cipher = Cipher.getInstance("DESede/CBC/PKCS5Padding");
			IvParameterSpec ips = new IvParameterSpec(keyiv);
			cipher.init(Cipher.ENCRYPT_MODE, convertSecretKey,ips);
			byte[] result = cipher.doFinal(str.getBytes());
			returnStr = Base64.encodeBase64String(result);
		} catch (Exception e) {
		}
		return returnStr;
	}

	/**
	 * decrypt
	 * 
	 * @param str 待解密字符串
	 * @param key 密钥
	 * @return
	 */
	public static String decrypt(String str, String key) {
		String returnStr = "";
		try {
			// key转换
			DESedeKeySpec deSedeKeySpec = new DESedeKeySpec(key.getBytes());
			SecretKeyFactory factory = SecretKeyFactory.getInstance("DESede");
			Key convertSecretKey = factory.generateSecret(deSedeKeySpec);
			Cipher cipher = Cipher.getInstance("DESede/CBC/PKCS5Padding");
			IvParameterSpec ips = new IvParameterSpec(keyiv);
			cipher.init(Cipher.DECRYPT_MODE, convertSecretKey,ips);
			byte[] result = cipher.doFinal(Base64.decodeBase64(str.getBytes()));
			// System.out.println(Base64.encodeBase64(result));
			System.out.println("decrypt : " + new String(result));
			returnStr = new String(result, "UTF-8");
		} catch (Exception e) {
			e.printStackTrace();
		}
		return returnStr;
	}

	/**
	 * read file
	 * @param path
	 * @return
	 * @throws Exception
	 */
	public static String readFile(String path) throws Exception {
		File f = new File(path);
		InputStream in = new FileInputStream(f);
		byte[] b = new byte[(int) f.length()];
		for (int i = 0; i < b.length; i++) {
			b[i] = (byte) in.read();
		}
		in.close();
		System.out.println(new String(b));
		return new String(b);
	}
	
	/**
	 * write file
	 * @param str
	 * @param path
	 */
	public static void writeFile(String str,String path){
		 File f=new File(path);
	        try{
	            f.createNewFile();
	            OutputStream out =new FileOutputStream(f);
	            byte[] b=str.getBytes();
	            for (int i = 0; i < b.length; i++) {
	                out.write(b[i]);
	            }
	            out.close();
	            
	        }catch (Exception e) {
	            e.printStackTrace();
	        }
	}

	public static void main(String[] args) {
		String keyStr = "hello world";
		String key = generateKeyByMd5(keyStr);
		System.out.println("key ：" + key);
//
//		System.out.println("加密后内容：" + encrypt3Des("hello", key));
//		System.out.println("解密后内容:" + decrypt("6ca8bd1aba93714e", key));
//		System.out.println("------------");
//		System.out.println(decrypt(encrypt3Des(
//				"hellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrdhellowolrd",
//				key), key));
	
		// 加密
		
		try {
			String str = readFile("/home/jay/test");
			str = encrypt3Des(str, key);
			System.out.println("加密后内容：" + str);
			writeFile(str,"/home/jay/output");
		} catch (Exception e) {
			e.printStackTrace();
		}
		
		// 解密
		try {
			String str = readFile("/home/jay/output");
			str = decrypt(str, key);
			System.out.println("解密后内容：" + str);
			writeFile(str,"/home/jay/output2");
		} catch (Exception e) {
			e.printStackTrace();
		}
		
	}
}

~~~
