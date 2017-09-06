# Xamarin

My notes and hints for Xamarin cross-platform development.

## Forms

### Toolkits

* [FormsCommunityToolkit/FormsCommunityToolkit](https://github.com/FormsCommunityToolkit/FormsCommunityToolkit)
The Forms Community Toolkit is a collection of Behaviors, Converters, and Effects for Xamarin.Forms. It simplifies and demonstrates common developer tasks building iOS, Android, and UWP apps with Xamarin.Forms.

### OnPlatform Examples

#### Making a Grid Row Definition per Platform

```xml
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition>
                <RowDefinition.Height>
                    <OnPlatform x:TypeArguments="GridLength" iOS="20" Android="8" />
                </RowDefinition.Height>
            </RowDefinition>            
            <RowDefinition Height="1*"/>
            <RowDefinition Height="2*"/>
            <RowDefinition Height="1*"/>
            <RowDefinition Height="30"/>
        </Grid.RowDefinitions>
    </Grid>
```

**x:TypeArguments** must match the public property type exactly. Otherwise a XAML compilation error will occurr. For the public property type check the class reference, for this example: https://developer.xamarin.com/api/type/Xamarin.Forms.RowDefinition/ you'll see that height is of type **GridLength**.

All public properties can have such configuration given you use the dot (.) notation above.

More examples can be found on this forum thread: https://forums.xamarin.com/discussion/47984/onplatform-xaml. Just have some time ensuring that the **x:TypeArguments** are correct.

Source: [Xamarin Forum Comment](https://forums.xamarin.com/discussion/comment/148203/#Comment_148203)


## iOS


## Android

### Make Android button labels not all-CAPS

Add the following to the **styles.xml** file, inside the Android project. It works for Xamarin.Android and Xamarin.Forms as well.

```xml
<style name="MyTheme" parent="@android:style/Theme.Material.Light.DarkActionBar">
        <item name="android:textAppearanceButton">@style/MyTextAppearance.Material.Button</item>
</style>

<style name="MyTextAppearance.Material.Button" parent="@android:style/TextAppearance.Material.Button">
        <item name="textAllCaps">false</item>
        <item name="android:textAllCaps">false</item>
</style>
```

Source: [Xamarin Forum Comment](https://forums.xamarin.com/discussion/comment/114645/#Comment_114645)

### Make Android buttons' background and border color transparent

```xml
<Button Image="Images/logout.png" Clicked="LogoutButton_OnClicked"
               HorizontalOptions="End"
                BorderColor="Transparent"
                BackgroundColor="Transparent"
                Scale="0.5"/>
```

Source: [Xamarin Forum Comment](https://forums.xamarin.com/discussion/63850/android-button-how-to-make-transparent-background-and-no-border)

### Remove the shadow around the Android button

Add the following to the **styles.xml** file, inside the Android project. It works for Xamarin.Android and Xamarin.Forms as well.

```xml
	<style name="MyTheme" parent="MyTheme.Base">
		<!--Reference: https://forums.xamarin.com/discussion/comment/114645/#Comment_114645-->
		<item name="android:textAppearanceButton">@style/NoCaps.Material.Button</item>
		<!--Reference: https://forums.xamarin.com/discussion/comment/215760/#Comment_215760-->
		<item name="android:buttonStyle">@style/NoShadowButton</item>
	</style>

    <!--Reference: https://forums.xamarin.com/discussion/comment/215760/#Comment_215760-->
	<style name="NoShadowButton" parent="android:style/Widget.Button">
        <item name="android:stateListAnimator">@null</item>
    </style>
```

Source: [Xamarin Forum Comment](https://forums.xamarin.com/discussion/comment/215760/#Comment_215760)