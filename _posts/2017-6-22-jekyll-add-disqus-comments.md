---  
layout: post  
title:  "为Jekyll增添多说评论"  
date:   2017-6-22 22:01:19  
categories: jekyll  
---  
在做以下步骤之前，先去 [duoshuo.com](https://duoshuo.com) 上注册一个帐号，获取 `short_name`

首先按照如下格式编辑 `_config.yml`


<pre class="brush:java;">
  comments :
     provider : duoshuo
     duoshuo :
          short_name : havee
          
          </pre>
        
    
其次进入 `_includes/` 目录创建目录 `custom` 以及在刚创建的 `custom` 目录下创建文件 `duoshuo`    


   <pre class="brush:bash shell;">
      $ cd _includes; mkdir custom; cd custom ; touch duoshuo
   </pre>
 
 填充如下内容
 
 <pre class="brush:bash shell;"> 
    <!-- Duoshuo Comment BEGIN -->
     <div id="comments">
        <div class="ds-thread" {% if page.id %}data-thread-key="{{ page.id }}"{% endif %}  data-title="{% if page.title %}{{ page.title }} - {% endif %}{{ site.title }}"></div>
    </div>
  <!-- Duoshuo Comment END -->
  </pre>
 
 由于同一页面调用多个多说系统的数据，其 `js` 只需加载一次即可。所以相关的 `javascript` 我们放到默认的 `default` 中，编辑 `_includes/themes/havee/default.html` 文件，在
 
   <pre class="brush:bash shell;">
     {% include JB/analytics %}
   </pre>
上面添加多说的 js 代码   
 
 <pre class="brush:javascript;">
  <!--多说js加载开始，一个页面只需要加载一次 -->
<script type="text/javascript">
  var duoshuoQuery = {short_name:"{{ site.JB.comments.duoshuo.short_name }}"};
  (function() {
    var ds = document.createElement('script');
    ds.type = 'text/javascript';ds.async = true;
    ds.src = 'http://static.duoshuo.com/embed.js';
    ds.charset = 'UTF-8';
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ds);
  })();
</script>
<!--多说js加载结束，一个页面只需要加载一次 -->
          
          </pre>
    

