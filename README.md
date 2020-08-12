# Xamarin Solutions
To track my solutions for Xamarin.Forms

### Shell
- [x] [Fully Custom tabbar](shell/shell-custom-tabbar.md) (support badge, colorfull icon etc)
- [ ] Scroll Position Reset Issues (on Android)
  - [Issues 1](https://github.com/xamarin/Xamarin.Forms/issues/8795), [Issues 2](https://github.com/xamarin/Xamarin.Forms/issues/10501)
  - Tried reset Scroll Position (include reflect method) but failed
  - No solution yet
- [x] ~~Custom Flyout Panel~~
  - **Update** : Bad user experence, use [Custom Side Drawer](shell/side-drawer.md) instead.
- [x] [Flyout right side](https://github.com/balbarak/xamarin-shell-rtl)

### ScrollView
- [x] To enable scroll
  - Padding > 0 (recommend 1 or 0.1, otherwise when stop may hide partical header)
  - If StackLayout as child, VerticalOptions<>"Start"
  - Set child's padding to keep space
- [x] Case layout over head when use as root
  - Wrap by AbsoluteLayout to fix it

### Frame
- [x] Corner Radius not show on iOS sometimes
  - Make sure child element has margin, same value (can only set XY) as CornerRadius
  - My case is StackLayout as child

### Side Drawer
- [x] [Custom Side Drawer](shell/side-drawer.md)
  - No render, no third party lib

### Erros
- [x] Specified cast is not valid
  - Check xaml bindings
  - Check if you push a page, with NavigationPage
  ``` C#
  await Navigation.PushAsync(new **NavigationPage**(new SomeContentPage()));
  ```
  
### Debug
- [x] [Android] data wiped everytime uninstall
  - Turn off backup via Settings -> System -> Backup, turn off whaterver backup provider(mine is Google Drive) 
