---
title: AsyncHttpClient 用法
author: admin
layout: post
date: 2013-08-26
url: /asynchttpclient-用法/
categories:
  - 操作系统
tags:
  - AsyncHttpClient

---
<pre>import java.util.concurrent.Future;

import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.nio.client.CloseableHttpAsyncClient;
import org.apache.http.impl.nio.client.HttpAsyncClients;

public class AsyncClientHttpExchange {

    public static void main(final String[] args) throws Exception {
        final CloseableHttpAsyncClient httpclient = HttpAsyncClients.createDefault();
        httpclient.start();
        try {
            final HttpGet request = new HttpGet("http://www.apache.org/");
            final Future&lt;HttpResponse&gt; future = httpclient.execute(request, null);
            final HttpResponse response = future.get();
            System.out.println("Response: " + response.getStatusLine());
            System.out.println("Shutting down");
        } finally {
            httpclient.close();
        }
        System.out.println("Done");
    }

}

资源包下载：<a href="http://hc.apache.org/downloads.cgi">http://hc.apache.org/downloads.cgi</a></pre>