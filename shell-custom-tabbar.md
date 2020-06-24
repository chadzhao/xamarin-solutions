### Problem
> Orignal shell tabbar has limited support, no badge, no colorfull icon

- [Issues Link](https://github.com/xamarin/Xamarin.Forms/issues/6112)

### My Solution
- Use custom view to define Tabbar layout
  - use Grid to custom everything, includ badge, selected effort, colorfull image etc
  - switch Shell tab programmly
  - maintain status (such as badge) in serval tabbar instances
- Put new tabbar to every page in AppShell, use Grid to keep it at bottom
- Hide original tabbar in AppShell page (will keep hiding all times)

#### 1. Hide tab bar in AppShell page
``` xml
<Shell Shell.TabBarIsVisible="False">
  Your layout
</Shell>
```

It will keep hiding all time without manually hide in other page.

#### 2. Create your own tab bar view by creating a custom Grid view
``` xml
<Grid x:Class="MyLib.Views.MyTab" BackgroundColor="#2196F3" ColumnSpacing="0">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="*" />
    </Grid.ColumnDefinitions>

    # Tabbar layout
    <StackLayout Grid.Column="0" Padding="0,5,0,0" Orientation="Vertical">
        <Image Source="course.png" WidthRequest="30" HeightRequest="30"></Image>
        <Label Text="MyCourse" TextColor="White" HorizontalOptions="Center"></Label>
    </StackLayout>

    # Handle tapped, show badge, show selected mask
    <AbsoluteLayout Grid.Column="0" x:Name="lay0">
        <AbsoluteLayout.GestureRecognizers>
            <TapGestureRecognizer Tapped="OnSelected" CommandParameter="0"></TapGestureRecognizer>
        </AbsoluteLayout.GestureRecognizers>

        <Grid AbsoluteLayout.LayoutFlags="All" AbsoluteLayout.LayoutBounds="0,1,1,1" IsVisible="true" BackgroundColor="White" Opacity="0.2"></Grid>
        <Frame AbsoluteLayout.LayoutFlags="PositionProportional" AbsoluteLayout.LayoutBounds=".9,0.1,12,12" CornerRadius="6" BackgroundColor="#cf1322" Padding="0"></Frame>
    </AbsoluteLayout>

     Other Tabs Here
</Grid>
```
TIPS: MyLib.Views.MyTab needs to inherit from Grid.

#### 3. Add switch tab logic in MyTab.xaml.cs
``` c#
private void OnSelected(object sender, EventArgs e)
{
    if (e is TappedEventArgs tap)
    {
        var newIndex = Convert.ToInt32(tap.Parameter);
        var shell = Shell.Current;
        shell.CurrentItem.CurrentItem = shell.CurrentItem.Items[newIndex];
    }
}

int selectedIndex = -1;
public int SelectedIndex
{
    get { return selectedIndex; }
    set
    {
        if (selectedIndex != value)
        {
            selectedIndex = value;

            switch (value)
            {
                case 0: this.lay0.Children[0].IsVisible = false; break;
                case 1: this.lay1.Children[0].IsVisible = false; break;
                case 2: this.lay2.Children[0].IsVisible = false; break;
                case 3: this.lay3.Children[0].IsVisible = false; break;
            }
        }
    }
}

```

#### 4. Add MyTab to all tab pages which shown in AppShell page
``` xml
<Grid Margin="0" RowSpacing="0">
    <Grid.RowDefinitions>
        <RowDefinition />
        <RowDefinition Height="60" />
    </Grid.RowDefinitions>

    <local:MyTab Grid.Row="1" SelectedIndex="0"></local:MyTab>

     Your original page layout here
</Grid>
```

### Screenshots
#### On Android
![screenshot](https://user-images.githubusercontent.com/8391427/85477959-71e7c200-b60f-11ea-8afe-20005af3bdf6.gif)

### Advantage
- No custom render needed.
- **ALL Customized**, by using Grid(or others you prefer) for tabbar layout. 
  - Badge with/without number
  - Colorfull image as ICON, or colorfull image for selected tab
  - More
- Keep the same animation as iOS when open no tabbar page in Android
  - original Shell will hide tabbar before switch, not good

### Disadvantage
- Ideal for only use Shell in home page, other pages prefer to hide tabbar.
  - tabbar will come and go with each page
- Case a little lower performance but hard to detect
- Maintain the status between MyTab instances
