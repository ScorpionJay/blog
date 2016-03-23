title: Android list 自动高度
date: 2015-10-06 15:56:46
tags:
- android
---
Android list 自动高度
<!--more-->
~~~java
* auto set ListView height
 * 
 * @param listView
 */
public static void setListViewHeightBasedOnChildren(ListView listView) {
	if (listView == null)
		return;

	ListAdapter listAdapter = listView.getAdapter();
	if (listAdapter == null) {
		return;
	}

	int totalHeight = 0;
	for (int i = 0; i < listAdapter.getCount(); i++) {
		View listItem = listAdapter.getView(i, null, listView);
		listItem.measure(0, 0);
		totalHeight += listItem.getMeasuredHeight();
	}

	ViewGroup.LayoutParams params = listView.getLayoutParams();
	params.height = totalHeight
			+ (listView.getDividerHeight() * (listAdapter.getCount() - 1));
	listView.setLayoutParams(params);
}
~~~


----------


注意
	布局需要是LinearLayout