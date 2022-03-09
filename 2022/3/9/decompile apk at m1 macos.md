# Decompile apk at m1 macos

## Tools
```bash
brew install apktool 

brew install dex2jar
#d2j-dex2ja
```

## Get apk source file
```bash
apktool d **.apk
```

## Get jar file
```bash
d2j-dex2jar **.apk
```

## View jar
http://www.javadecompilers.com/


## When you meet `odex`
You can get the `odex` file from the android system image, for example, the .img file

https://www.jianshu.com/p/22afbc58b6b8