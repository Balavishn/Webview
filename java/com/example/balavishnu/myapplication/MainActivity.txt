package com.example.balavishnu.myapplication;

import android.content.Intent;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.support.v4.content.ContextCompat;
import android.support.v7.app.AppCompatActivity;
import android.util.Log;
import android.view.View;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;
import android.widget.TextView;

import java.net.URISyntaxException;


public class MainActivity extends AppCompatActivity {
    Button btnStartService, btnStopService;
    WebView web;
    String url="";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
     //   TextView t1=(TextView)findViewById(R.id.t1);
      //  t1.setText(url);
       web=(WebView)findViewById(R.id.web);
       web.setWebViewClient(new WebViewClient());
       web.loadUrl("https://www.google.com/");
       startService(new Intent(this,ClipboardMonitorService.class));
       Intent i=getIntent();
       url=i.getStringExtra("copiedLink");
       web.loadUrl(url);
       web.getSettings().getJavaScriptEnabled();
       web.setWebViewClient(new WebViewClient(){

            @Override
            public void onPageStarted(WebView view, String url, Bitmap favicon) {
                super.onPageStarted(view, url, favicon);
            }

            @Override
            public void onPageFinished(WebView view, String url) {
                super.onPageFinished(view, url);
            }
        });


    }

    @Override
    public void onBackPressed() {
        if(web.canGoBack()){
            web.goBack();
        }
        else{
        super.onBackPressed();
        }
    }
}
