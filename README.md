This is the example of my [Android Inline Hook Project](https://github.com/GToad/Android_Inline_Hook.git) in thumb mode.

The target APP is `thumb-2-example.apk` and our .so file has already been compiled in `/libs/armeabi-v7a/libInlineThumbHook.so`.

In this APP, you should wait for more than 30 seconds and it will show `Enough. You Win!` in the middle of the screen. After the example `libInlineThumbHook.so` is effective, the register R0 will be set to 0x333 (>10) so you will get `Enough. You Win!` immediately.

`notThumbHooked.mp4` shows the APP run in a normal environment.

`ThumbHooked.mp4` shows the APP run in a hooked environment.

The pictures of effect are showed below:

![](https://gtoad.github.io/img/in-post/post-android-native-hook-practice/notThumbHooked.png)
![](https://gtoad.github.io/img/in-post/post-android-native-hook-practice/ThumbHooked.png)

# Android Inline Hook

This project make an Android .so file that can automatically do some native hook works.

It mainly use Android Inline Hook, not PLT Hook.

If you can read Chinese or wanna see more picture, I've wrote some articles about this repo and the first one is the main article.

1. [Android Inline Hook Practice](https://gtoad.github.io/2018/07/06/Android-Native-Hook-Practice/)
2. [Opcode Fix In Android Inline Hook](https://gtoad.github.io/2018/07/13/Android-Inline-Hook-Fix/)
3. [An Introduction to Android Native Hook](https://gtoad.github.io/2018/07/05/Android-Native-Hook/)

# How To Use

The only thing you have to change is the code in `InlineHook.cpp`.

You can name the `__attribute__((constructor)) ModifyIBored()` function at your will and change the follow arg in it:

1. `pModuleBaseAddr` is the address of your target so.
2. `target_offset` is the offset of your hook point in the target so.
3. `is_target_thumb` shows the hook point's CPU mode. You can know this information in the work of reversing before the hook work.

`EvilHookStubFunctionForIBored` function is the thing you really wanna do when the hook works. You can name at your will, but keep the arg `(pt_regs *regs)`. It brings you the power to control the registers, like set r0 to 0x333 : `regs->uregs[0]=0x333;`.

# Example

I've make some examples in other repo, it includes code and the target APK file.

1. [thumb-2 example](https://github.com/GToad/Android_Inline_Hook_Thumb_Example.git)
2. [arm32 example](https://github.com/GToad/Android_Inline_Hook_Arm_Example.git)

# Contact

I believe that this project still has some problems. If you find some bugs or have some problems, you can send e-mail to `gtoad1994@aliyun.com`. I wish we can fix it together!

# Reference

[Game Security Lab of Tencent](http://gslab.qq.com/portal.php?mod=view&aid=168)

[Ele7enxxh's Blog](http://ele7enxxh.com/Android-Arm-Inline-Hook.html)




