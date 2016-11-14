欢迎您使用byLoader
===
##插件简介
        byLoader用于加载css及js文档,当前版本为v0.00.012,他有如下特点:
        1.可以实现一个script标签加载页面所需的全部css及js文档;
        2.对加载文档进行缓存可控化,每两个小时更新一次(需要设置参数),防止版本迭代时不能及时更新页面;
        3.当页面刷新或者重新载入时,会从缓存中优先读取,缩短响应时间,减少页面载入时的闪烁;
        4.减少服务器请求数量;
        5.减少客户端网络流量;
        6.外网自动加载文档的.min版本,内网加载正常版本,开发及上线一气呵成,减少维护成本.
##使用方法(任选其一)
        1.标签属性定义法(推荐):
         <script type="text/javascript" data-dir="/media/user/" data-css="public/global,public/color,other,_css" data-js="libs/jquery-3.1.0,libs/jquery.byAlert,_js" data-update-version=false src="/media/user/js/libs/byLoader.min.js"></script>
        
        2.命令行语句法:
        <script type="text/javascript" src="/media/user/js/libs/byLoader.js"></script>
        <script type="text/javascript">
          var loader=new byLoader();
          loader.dataDir="/media/user/";
          loader.dataCss=['public/global','public/color','other','_css'];
          loader.dataJs=['libs/jquery-1.8.0','libs/jquery.byAlert','_js'];
          loader.updateVersion=false;//默认为false
          loader.callBack=function(){console.log("byLoader is done!")};   //外部命令法可以定义回调函数
          loader.run();
        </script>
        当然,您也可以写成这样:
        <script type="text/javascript">
          var loader=new byLoader({
            dataDir:"/media/users/",
            dataCss:['public/global','public/color','other','_css'],
            dataJs:['libs/jquery-1.8.0','libs/jquery.byAlert','_js'],
            updateVersion:true,//默认为false
            callBack:function(){console.log("byLoader is done!")}   //外部命令法可以定义回调函数
          });
          loader.run();
        </script>
##使用说明
        1.在页面的合适位置插入javascript标签
        2.javascript标签的"data-dir"属性定义模块的基础路径(*可选)[默认值:'./'];
        3.javascript标签的"data-css"属性定义css模块,多个css以逗号分割,byLoader会依次加载,不需要指定文件的扩展名称(*可选)[默认值:'']
        4.javascript标签的"data-js"属性定义js模块,多个js以逗号分割,byLoader会依次加载,不需要指定文件的扩展名称(*可选)[默认值:''];
        5.javascript标签的"data-update-version"属性定义是否更新本地缓存的版本号(*可选)[默认值:false];
        6.标签属性定义法与命令行语句法中的属性名称分别如下一一对应:
            data-dir  相当于 dataDir
            data-css 相当于 dataCss
            data-js    相当于 dataJs
            data-update-version 相当于updateVersion
        7.命令行语句法可以定义回调函数,标签属性定义法不支持定义回调函数
##注意事项
        1.由于本插件需要使用localStorage功能,所以必须是现代浏览器或者IE10以上版本才可以成功运行;
        2.css模块的路径在基础路径下的"css"目录中,js模块的路径在基础路径下的"js"目录中;
        3.当data-css包含"_css"模块时,代表byLoader自动加载页面css,例如当页面为127.0.0.1/index/index.html,则对应的css为127.0.0.1/[data-dir]/css/index/index.css;;
        4.当data-js包含"_js"模块时,代表byLoader自动加载页面js,例如当页面为127.0.0.1/index/index.html,则对应的js为127.0.0.1/[data-dir]/js/index/index.js;
        5.支持require.js,当data-js中包含"require"模块时,则会自动为require的data-main属性自动定义为[data-dir]/js/modules/index/index,正因如此,data-main模块将脱离byLoader缓存机制;
        6.data-update-version属性定义是否更新本地缓存的数据版本号,更新版本号会让程序认为缓存数据是最新的(版本号为"00000"时除外),从而在下次更新版本号之前可以优先从缓存中读取,注意当有多个byLoader实例同时执行时,只需在最后一个执行时设置为true,因为连续更新缓存版本,会误导后面的版本判断,如果只有一个byLoader实例运行时,建议将此参数值设置为true;
        7.如果是公有IP或者非localhost,所加载的文档会直接从localStorage中读取(需要定义data-update-version=true),并且每两个小时更新一次;
        8.如果是私有IP或者localhost,为了开发调试方便每刷新一次更新一次,由此加载速度较慢,请知晓;
        9.请使用相关压缩程序将js及css进行压缩成"min"版本,建议使用YUI Compressor;
        10.当使用byLoader.js时,在本地开发环境下会以console.log()命令友情提示,如果不希望出现提示请使用byLoader.min.js.
##更多...
        https://github.com/baiyukey/byLoader
        作者:龙马印
        联系方式:baiyukey@hotmail.com
