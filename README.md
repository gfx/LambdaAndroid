## LetroLambda works on Android!

祝！Java8 release（2014/3/18）！lambda式バンザイ！

lambda式はcallback styleのAPIと非常に相性がいいので、これからのMBaaS SDK設計は大きく変わるはず。

[@zaki50: retrolambda https://github.com/evant/gradle-retrolambda … 組み込んだ gradle のプロジェクトにしたら Android で lambda 使えた！ https://gist.github.com/zaki50/c16db7cb29cee0a5e364 … ](https://twitter.com/zaki50/status/445569652941258752)

https://github.com/evant/gradle-retrolambda

というわけで、retrolambdaを使ってAndroidでλ式を使ってみました。

`app/build.gradle` をちょろっと設定するだけで…

```groovy
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'me.tatarka:gradle-retrolambda:1.3.0'
    }
}


apply plugin: 'android'
apply plugin: 'retrolambda'

retrolambda {
    jdk "/Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home"
}

android {
	...

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

	...
}

```

`minSdkVersion 8` でも lambda式が使える！YATTA！

```java
findViewById(R.id.hello).setOnClickListener((view) -> {
	Toast.makeText(getApplication(), "Yeah!", Toast.LENGTH_LONG).show();
});
```
