# tuyou
项目实现了一个基于LBS和混合推荐算法的智能旅游导游系统。项目系统包括Android app（客户端）与服务器后台（服务端），其中客户端包括地图、导览等功能，服务端为客户端提供数据存储、查询等功能的接口，以及为用户提供兴趣计算的能力。

项目中应用的关键技术：UI/UX及可用性设计、Android编程、Kotlin开发、Android特色开发基于位置的服务、数据库架构设计、服务器leancloud开发。



## 主要功能

1. 查看地图
2. 显示用户地理位置
3. 搜索景点
4. 智能推荐景点
5. 实时语音导览
6. 收藏自己喜欢的景点





通过构造的兴趣向量和 收藏* （收藏/总数）进行优先级排序，然后对最感兴趣的方面，进行lbs的定位搜索附近的景点，然后进行前5个进行路线连接规划。

你想去哪里，规划从这个地方到你想去地方之前的距离之间的所有分类的爱好进行标注。推荐从数据库中找到没有被收藏，同时是你的爱好的

### 用户表 User



| 字段              | 描述     | 类型   |
| ----------------- | -------- | ------ |
| mobilePhoneNumber | 手机号   | String |
| userFav           | 兴趣表id | String |

### 用户兴趣表 UserFav

用户兴趣表存储用户的兴趣信息。

| 字段         | 描述               | 类型   |
| ------------ | ------------------ | ------ |
| userObjectId | 用户id             | String |
| interest     | 兴趣向量           | Array  |//不同收藏下的点击数
| favList      | 收藏总数           | Int    |
| favAmount    | 每个分类下的收藏数 | Array  |//分类下的收藏多少

### 标签列表 TagInfo

标签列表存储所有标签，便于在首页调取展示。

| 字段    | 描述     | 类型   |
| ------- | -------- | ------ |
| tagId   | 标签序号 | Int    |//对每个景点进行标签
| tagName | 标签名称 | String |

### 分类列表 Category

分类列表存储了所有分类，用于计算兴趣向量等。

| 字段         | 描述     | 类型   |
| ------------ | -------- | ------ |
| categoryId   | 分类序号 | Int    |
| categoryName | 分类名称 | String |

### 景点列表 PlaceInfo

景点列表存储了景点信息，用于数据的展示、查询。

| 字段     | 描述         | 类型        |
| -------- | ------------ | ----------- |
| id       | 景点id       | String      |
| name     | 景点名称     | String      |
| desc     | 景点描述     | String      |
| imgSrc   | 景点图片地址 | String      |
| tags     | 景点标签     | Array       |
| location | 景点坐标     | GeoLocation |
| category | 景点分类     | Array       |


### 用户收藏日志 FavoriteLog

用户收藏日志记录所有用户的收藏信息。

| 字段         | 描述                           | 类型   |
| ------------ | ------------------------------ | ------ |
| type         | 收藏类别（为景点） | Int    |  //可能会有兴趣点，和景点，现在就是景点信息
| favId        | 收藏id                         | String |//收藏的景点信息
| user         | 用户名                         | String |
| userObjectId | 用户id                         | String |//是哪一个用户
| userFav      | 用户所在兴趣表id               | String | // 代表用户的兴趣表示哪一个
	
### 用户搜索日志 SearchLog

用户搜索日志记录所有用户的搜索信息。

| 字段       | 描述   | 类型   |
| ---------- | ------ | ------ |
| user       | 用户名 | String |
| searchText | 搜索词 | String |
