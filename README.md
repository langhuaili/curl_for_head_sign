# curl_for_head_sign
a way to  use curl skills to get the passage of a webiste
<?php 

function show_side($tgurl){
$wwwtext=get_url_content($tgurl);
$str=$wwwtext;

//取head标签内容
preg_match("/<title>(.*)<\/title>/si",$str,$match);
 $headstr = trim($match[1]);
 //return $headstr;
echo '<li><a href="'.$tgurl.'">'.$headstr.'</a></li>';
}



function get_url_content($url){
    if(function_exists("curl_init")){
        $ch = curl_init();
        $timeout = 60;
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
       // curl_setopt($ch, CURLOPT_NOBODY, 1);
        curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, $timeout);
        $str = curl_exec($ch);
        curl_close($ch);
    }else{
        if(ini_get('allow_url_fopen')){$str = file_get_contents($url);}
    }
    return $str;
}



//配置URL
$url = array('http://www.ifeng.com/','http://www.baidu.com/','http://www.ifeng.com/','http://www.baidu.com/','http://www.ifeng.com/','http://www.baidu.com/'
    );


 foreach ($url as $value) {
             show_side($value);}
 



