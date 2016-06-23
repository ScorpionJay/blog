---
title: React Native Navigator
date: 2016-06-22 13:04:31
tags:
- react native
---

react native navigator
<!--more-->
https://github.com/exponentjs/react-native-tab-navigator
http://www.tuicool.com/articles/A3eUZr


npm 

import TabNavigator from 'react-native-tab-navigator'
~~~
      <TabNavigator tabBarStyle={{ height: tabBarHeight, overflow: 'hidden' }}
  sceneStyle={{ paddingBottom: tabBarHeight }} >
        <TabNavigator.Item
          selected={this.state.selectedTab === 'Home'}
          title="首页"
          renderIcon={() => <Image source={require('./images/star2.png')} style= {styles.img}/>}
          renderSelectedIcon={() => <Image source={require('./images/star1.png')} style= {styles.img}/>}
          onPress={() => this.setState({ selectedTab: 'Home' })}>
          <Find/>
        </TabNavigator.Item>
        <TabNavigator.Item
          selected={this.state.selectedTab === 'Me'}
          title="我"
          renderIcon={() => <Image source={require('./images/me2.png')} style= {styles.img}/>}
          renderSelectedIcon={() => <Image source={require('./images/me1.png')} style= {styles.img}/>}
          onPress={() => this.setState({ selectedTab: 'Me' })}>
           <Me />
        </TabNavigator.Item>

      </TabNavigator>
~~~
