// ==UserScript==
// @name         ygn - isim kopyalama
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  gartic isim kopyalama
// @author       ygn
// @grant        none
// @match        *://gartic.io/*
// ==/UserScript==
function ygn(x,y="boş"){
	if(x.indexOf(" ")==-1){
    	if(y=="boş"){
        	return document.querySelectorAll(x);
        }else{
        	return document.querySelectorAll(x)[y];
        }
    }else{
    	return document.getElementsByClassName(x);
    }
}
window.copyName=function(){
    name = ygn(".contentPopup")[0].innerText;
    ygn("input",4).value = name;
    ygn("#ccbtn")[0].innerHTML = "<strong>KOPYALANDI!</strong>";
    ygn("input",4).value = " " + name;
    ygn("input",4).select();
    document.execCommand("copy");
    ygn("input",4).value = "";
}
if(window.location.href.indexOf("viewer")==-1){
    var c,profileon=0,name;

    if(window.location.href.indexOf("https://gartic.io/")!==-1 && window.location.href.indexOf("croxy")==-1 && window.location.href.indexOf("?bot")==-1){
        setInterval(function(){
            if(ygn("content profile").length > 0 && profileon==0){
                profileon=1;
                var copyNameButton = '<button id="ccbtn" class="btYellowBig" onclick="copyName()"><strong>ADI KOPYALA</strong></button>';
                ygn(".buttons")[0].innerHTML+=copyNameButton;
            }

            if(ygn("content profile").length ==0){
                profileon=0;
            }
        },100);
    }
}
