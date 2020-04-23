# How to get an AccordionItem in Xamarin.Forms (SfAccordion)

You can get which [AccordionItem](https://help.syncfusion.com/cr/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Accordion.AccordionItem.html?) is expanded or collapsed using [ClassId](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.element.classid?view=xamarin-forms) in Xamarin.Forms.

You can also refer the following article.

https://www.syncfusion.com/kb/11439/how-to-get-an-accordionitem-in-xamarin-forms-sfaccordion

**XAML**

Binding **ClassId** in **AccordionItem**
``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:syncfusion="clr-namespace:Syncfusion.XForms.Accordion;assembly=Syncfusion.Expander.XForms"
             x:Class="AccordionXamarin.MainPage”>
 
    <ContentPage.Content>
        <syncfusion:SfAccordion x:Name="Accordion" ExpandMode="SingleOrNone" Margin="5" BindableLayout.ItemsSource="{Binding Info}">
            <syncfusion:SfAccordion.Behaviors>
                <local:Behavior/>
            </syncfusion:SfAccordion.Behaviors>
            <BindableLayout.ItemTemplate>
                <DataTemplate>
                    <syncfusion:AccordionItem x:Name="AccordionItem" ClassId="{Binding ClassID}">
                        <syncfusion:AccordionItem.Header>
                            <Grid HeightRequest="50">
                                <Label Text="{Binding Name}" VerticalOptions="Center" HorizontalOptions="StartAndExpand"/>
                            </Grid>
                        </syncfusion:AccordionItem.Header>
                        <syncfusion:AccordionItem.Content>
                            <Grid Padding="5" BackgroundColor="NavajoWhite">
                                <Label Text="{Binding Description}"/>
                            </Grid>
                        </syncfusion:AccordionItem.Content>
                    </syncfusion:AccordionItem>
                </DataTemplate>
            </BindableLayout.ItemTemplate>
        </syncfusion:SfAccordion>
    </ContentPage.Content>
</ContentPage>
```
**C#**

Perform operation based on **ClassId**
``` c#
namespace AccordionXamarin
{
    public class Behavior : Behavior<SfAccordion>
    {
        SfAccordion Accordion;
        protected override void OnAttachedTo(SfAccordion bindable)
        {
            Accordion = bindable;
            Accordion.Expanded += Bindable_Expanded;
            Accordion.Collapsed += Bindable_Collapsed;
            base.OnAttachedTo(bindable);
        }
 
        private void Bindable_Expanded(object sender, ExpandedAndCollapsedEventArgs e)
        {
            var index = e.Index;
            var item = Accordion.Items[index];
            if (item.ClassId =="Item1")
            {
                App.Current.MainPage.DisplayAlert("Informtion", "Accordion Item1 Expanded", "Ok");
            }
            else if (item.ClassId == "Item2")
            {
                App.Current.MainPage.DisplayAlert("Informtion", "Accordion Item2 Expanded", "Ok");
            }
            else if (item.ClassId == "Item3")
            {
                App.Current.MainPage.DisplayAlert("Informtion", "Accordion Item3 Expanded", "Ok");
            }
            else if (item.ClassId == "Item4")
            {
                App.Current.MainPage.DisplayAlert("Informtion", "Accordion Item4 Expanded", "Ok");
            }
        }
 
        private void Bindable_Collapsed(object sender, ExpandedAndCollapsedEventArgs e)
        {
        }
 
        protected override void OnDetachingFrom(SfAccordion bindable)
        {
            Accordion.Expanded -= Bindable_Expanded;
            Accordion.Collapsed -= Bindable_Collapsed;
            Accordion = null;
            base.OnDetachingFrom(bindable);
        }
    }
}
```
**Output**

![AccordionItemClassID](https://github.com/SyncfusionExamples/accordion-item-classid-xamarin/blob/master/ScreenShots/AccordionItemClassID.gif)
