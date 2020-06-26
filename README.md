# Xamarin Solutions
To track my solutions for Xamarin.Forms

### Shell
- [x] [Fully Custom tabbar](shell/shell-custom-tabbar.md) (support badge, colorfull icon etc)
- [ ] Scroll Position Reset Issues (on Android)
  - [Issues 1](https://github.com/xamarin/Xamarin.Forms/issues/8795), [Issues 2](https://github.com/xamarin/Xamarin.Forms/issues/10501)
  - Tried reset Scroll Position (include reflect method) but failed
  - No solution yet
- [x] Custom Flyout Panel
  - Manually set Shell.FlyoutHeader's HeightRequest = Application.Current.MainPage.Height
  - Then all flyout filled with your custom content view
  - Use Shell.Current.FlyoutIsPresented = true/false to hide or open

### ScrollView
- [x] To enable scroll
  - Padding > 0 (recommend 1 or 0.1, otherwise when stop may hide partical header)
  - If StackLayout as child, VerticalOptions<>"Start"
  - Set child's padding to keep space
