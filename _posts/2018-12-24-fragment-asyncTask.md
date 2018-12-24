---
layout: post
title: Fragment에서 AsyncTask 실행문제
date: 2018-12-24 18:10:20 +0300
description:
img:
tags: [Android, Fragment, AsyncTask]
---
<br>

## Fragment에서 AsyncTask를 실행할 때 문제가 발생할 수 있다??
AsyncTask 실행 도중에 백 키나 뒤로가기로 액티비티를 종료하면 Fragment는 액티비티와 분리되면서 getContext()나 getActivity() 메소드가 null을 리턴합니다.  

AsyncTask의 onPostExecute()에서 Context를 사용할 때 NPE가 발생하므로, 권장되는 방식은 onPostExecute() 메소드 시작 부분에 getContext()나 getActivity()가 null이면 곧바로 리턴하게 하는 것입니다.

## AsyncTask 취소
AsyncTask에는 cancel() 메소드가 있습니다. cancel()을 호출하면 AsyncTask의 mCancelled 변수를 true로 만들고 쓰레드 작업 이후에 onPostExcute()대신 onCancelled()메소드를 호출합니다.  

쓰레드 작업이 오래 걸리는 경우에 doInBackground()메소드에서는 중간에 isCancelled()메소드로 체크해서 바로 리턴하는 로직이 권장됩니다.  

결론적으로 AsyncTask를 액티비티 종료 시점에 근접하게 종료하는 방법은 isCancelled() 리턴값을 doInBackground() 곳곳에서 체크하고(특히 반복문), AsyncTask를 멤버 변수로 유지하고서 Activity의 onDestroy()에서 AsyncTask의 cancel() 메소드를 호출하는 것입니다.  

<br>
<br>

> 원본은 '안드로이드 프로그래밍 NextStep' 책에서 확인하실 수 있습니다.