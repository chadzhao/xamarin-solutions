### Side Drawer

#### Solution 1 ~~Custom Flyout Panel~~
- On appShell.PropertyChanged, if(e.PropertyName == nameof(Height)) flyoutHeader.HeightRequest = appShell.Height;
- Then all flyout filled with your custom content view
- Use Shell.Current.FlyoutIsPresented = true/false to open or hide
- **Update** : Bad user experence, use custom layout instead.
  - On iOS, no animation
  - Only apear at left side (support right side but need renderer)
  
#### Solution 2 Use Custom Code
- Dynamic add Grid into page's root element (for easy use, force Grid as root ele), to
  - dynamic create and load sider drawer's conent, which definted by each page
  - make sider drawer grid full in parent (dynamic set rowspan and columnspan, according root grid)
  - add a shadow grid into root grid, behined of side drawer grid, also make it full in parent
  - make shadow invisiable, move side drawer out of screen
- when open side drawer
  - make animation to change sadow's Opcacity from 0 to 0.7 `FadeTo()`
  - sametime (no await) move side drawer to (0,0) position
  - you can deinfe direction to make different affects
- deinfine your layout in custom view
  - extends from Grid, etc
  - set Grid backgroud transparent, align your side drawer's content to any position, you can make lots possible, as:
    - side drawer apear from top, dynamic height
    - traditional left side, dynamic or fixed width
    - apear from bottom, dynamic height
    - apear from top, conent keep at top right, wrap by frame to make corner radius, make it more beautiful
- then you can dynamic create your custom view and show in the side drawer
- finally, make extension method for ContentPage, include all logic, make it easy to use the side drawer.
``` C#
public async static Task ToggleSider<TView>(this ContentPage page, SiderPosition position = SiderPosition.Left) 
  where TView : View, new()
{
   // find or create side drawer's grid in page's root Grid
   // open or close the side drawer
}

 public async static Task OpenSider<TView>(this ContentPage page, SiderPosition position = SiderPosition.Left) 
   where TView : View, new()
 {
 }
 
 public async static Task CloseSider(this ContentPage page)
 {
 }
 
 public async static Task CloseSider(this View view)
 {
 }
```
- then you only need to call
``` C#
// in ContentPage
await this.ToggleSider<MySiderView>(SiderPosition.Top);

// in MySiderView
await this.CloseSider();
```
