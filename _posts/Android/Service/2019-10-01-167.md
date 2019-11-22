---
layout: post
title: Bindservice调用服务流程
category: Service
tags: [Service]
excerpt: Bindservice调用服务流程
---


## 在服务内部有一个方法需要我们调用 比如办证方法 ##


    
        @Override
        public void Certificate(int money) {
            if (money >50){
                Toast.makeText(CertificateService.this, "马上给你办证", Toast.LENGTH_SHORT).show();
            }else{
                Toast.makeText(CertificateService.this, "钱不够，办什么证", Toast.LENGTH_SHORT).show();
            }
        }


## 在服务内部声明一个中间人对象(IBinder实现类) ##

    
    class MyBinder extends Binder implements IServer {

        @Override
        public void Certificate(int money) {
            if (money >50){
                Toast.makeText(CertificateService.this, "马上给你办证", Toast.LENGTH_SHORT).show();
            }else{
                Toast.makeText(CertificateService.this, "钱不够，办什么证", Toast.LENGTH_SHORT).show();
            }
        }
    }

## 在服务的onBind方法里面把我们定义的中间人对象返回 ##

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return new MyBinder();
    }

## 在mainActivity里面调用bindService，目的是为了获取我们定义的中间人对象 ##

    
    
	
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        if (ActivityCompat.checkSelfPermission(this, str[0]) != PackageManager.PERMISSION_GRANTED || ActivityCompat.checkSelfPermission(this,
                str[1]) != PackageManager.PERMISSION_GRANTED || ActivityCompat.checkSelfPermission(this, str[2]) != PackageManager.PERMISSION_GRANTED || ActivityCompat.checkSelfPermission(this, str[3]) != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(this, str, 1);
        }
        Intent intent = new Intent(this, CertificateService.class);
        bindService(intent,new myServiceConnection(),BIND_AUTO_CREATE);
    }

	public void Certificate(View view) {
        mIServer.Certificate(300);
    }

    public class myServiceConnection implements ServiceConnection {

        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            mIServer = (IServer) service;
        }

        @Override
        public void onServiceDisconnected(ComponentName name) {

        }
    }


