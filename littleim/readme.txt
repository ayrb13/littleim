dbserver	数据库服务器
	封装mysql数据库接口，对下端提供一致性数据查询操作接口
	接口清单：
		获取昵称，头像信息
		获取群组信息
		获取离线消息
		获取离线文件，离线图片信息的key信息
loginserver	登陆服务器
	对外提供账户验证工作，提供分配token和消息服务器的功能
	接口清单：
		验证用户名密码有效性
		分配token给客户端
		通知msgserver用户的token和登陆信息
msgserver	信息服务器
	对外提供数据接收，发送等逻辑信息，通过心跳包维持登陆状态，转发用户消息给其他的msgserver
routeserver	转发服务器
	当msgserver在本地找不到相应的用户时，会把消息转发给route，route通过session服务器查询到用户所在msgserver后，转发给相应的msgserver，否则记录离线消息到数据库
tunnelserver	打洞服务器
	用户在线期间发送图片或视频等文件可不经过服务器，减少服务器压力。通过udp打洞方式来进行端对端的tcp数据传输
fileserver	文件服务器
	用于用户获取离线文件，聊天图片等信息