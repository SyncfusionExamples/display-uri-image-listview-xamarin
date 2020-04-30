# How to display URI images in Xamarin.Forms ListView (SfListView)

You can display [URI](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.uriimagesource?view=xamarin-forms) images in [SfListView](https://help.syncfusion.com/xamarin/listview/overview?) in Xamarin.Forms by loading [Image](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/images?tabs=windows) in [ItemTemplate](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~ItemTemplate.html?).

You can also refer the following article.

https://www.syncfusion.com/kb/11485/how-to-display-uri-images-in-xamarin-forms-listview-sflistview

**C#**

Defining **ContactImage** property in **Model**.
``` c#
namespace ListViewXamarin
{
    public class Contacts : INotifyPropertyChanged
    {
        private string image;
 
        public string ContactImage
        {
            get { return this.image; }
            set
            {
                this.image = value;
                this.RaisedOnPropertyChanged("ContactImage");
            }
        }
 
        public event PropertyChangedEventHandler PropertyChanged;
 
        public void RaisedOnPropertyChanged(string _PropertyName)
        {
            if (PropertyChanged != null)
            {
                PropertyChanged(this, new PropertyChangedEventArgs(_PropertyName));
            }
        }
    }
}
```
**C#**

Populating **ContactImage** in **ViewModel** with URI.
``` c#
namespace ListViewXamarin
{
    public class ContactsViewModel : INotifyPropertyChanged
    {
        
        public ObservableCollection<Contacts> contactsinfo { get; set; }
 
        public void GenerateInfo()
        {
            Random r = new Random();
            for (int i = 0; i < 40; i++)
            {
                var contact = new Contacts();
                contact.ContactImage = ""; //Your Url goes here
                contactsinfo.Add(contact);
            }
        }
 
        public event PropertyChangedEventHandler PropertyChanged;
 
        public void OnPropertyChanged(string name)
        {
            if (this.PropertyChanged != null)
                this.PropertyChanged(this, new PropertyChangedEventArgs(name));
        }
    }
}
```
**XAML**

Binding **ContactImage** property with Image **Source** property.
``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ListViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms"
             x:Class="ListViewXamarin.MainPage" Padding="{OnPlatform iOS='0,40,0,0'}">
    
    <ContentPage.BindingContext>
        <local:ContactsViewModel/>
    </ContentPage.BindingContext>
 
    <ContentPage.Content>
        <StackLayout>
            <syncfusion:SfListView x:Name="listView" ItemSpacing="1" AutoFitMode="Height" ItemsSource="{Binding contactsinfo}">
                <syncfusion:SfListView.ItemTemplate >
                    <DataTemplate>
                        <ViewCell>
                            <ViewCell.View>
                                <Grid x:Name="grid" RowSpacing="0">
                                    <Grid.RowDefinitions>
                                        <RowDefinition Height="*" />
                                        <RowDefinition Height="1" />
                                    </Grid.RowDefinitions>
                                    <Grid RowSpacing="0">
                                        <Grid.ColumnDefinitions>
                                            <ColumnDefinition Width="70" />
                                            <ColumnDefinition Width="*" />
                                        </Grid.ColumnDefinitions>
 
                                        <Frame CornerRadius="2" OutlineColor="Black" Padding="2" Margin="2" HasShadow="True">
                                            <Image HeightRequest="95" WidthRequest="95" HorizontalOptions="FillAndExpand" VerticalOptions="FillAndExpand" Aspect="AspectFit">
                                                <Image.Source>
                                                    <UriImageSource Uri="{Binding ContactImage}" CacheValidity="1" CachingEnabled="true"/>
                                                </Image.Source>
                                            </Image>
                                        </Frame>
 
                                        <Grid Grid.Column="1" RowSpacing="1" Padding="10,0,0,0" VerticalOptions="Center">
                                            <Grid.RowDefinitions>
                                                <RowDefinition Height="*" />
                                                <RowDefinition Height="*" />
                                            </Grid.RowDefinitions>
                                            <Label Text="{Binding ContactName}"/>
                                            <Label Grid.Row="1" Grid.Column="0" Text="{Binding ContactNumber}"/>
                                        </Grid>
                                    </Grid>
                                </Grid>
                            </ViewCell.View>
                        </ViewCell>
                    </DataTemplate>
                </syncfusion:SfListView.ItemTemplate>
            </syncfusion:SfListView>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```
