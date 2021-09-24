# How to display few cells of a columns have different foreground along with underline based on a condition in WPF DataGrid (SfDataGrid)?

This sample show cases how to apply the conditional styling for grid columns in [WPF DataGrid](https://www.syncfusion.com/wpf-ui-controls/datagrid) (SfDataGrid)?

# About the sample

You can apply the conditional styling for [GridColumn](https://help.syncfusion.com/cr/cref_files/wpf/Syncfusion.SfGrid.WPF~Syncfusion.UI.Xaml.Grid.GridColumn.html) by using converter and [CellTemplate](https://help.syncfusion.com/cr/cref_files/wpf/Syncfusion.SfGrid.WPF~Syncfusion.UI.Xaml.Grid.GridColumnBase~CellTemplate.html) in [WPF DataGrid](https://www.syncfusion.com/wpf-ui-controls/datagrid) (SfDataGrid).

```xml
<Window.Resources>
    <local:WbsElementToHyperLinkConverter x:Key="WbsElementToHyperLinkConverter"/>
</Window.Resources>

<syncfusion:GridTextColumn MappingName="OrderID" HeaderText="Order ID" AllowFiltering="False" MinimumWidth="10" Width="90" >
    <syncfusion:GridTextColumn.CellTemplate>
        <DataTemplate>
            <TextBlock  Text="{Binding Path=OrderID}"  
            TextDecorations="{Binding Converter={StaticResource WbsElementToHyperLinkConverter},ConverterParameter=TextDecorations}"  
            Foreground="{Binding Converter={StaticResource WbsElementToHyperLinkConverter},ConverterParameter=ForeGround}" />
        </DataTemplate>
    </syncfusion:GridTextColumn.CellTemplate>
</syncfusion:GridTextColumn>
```
```c#
public class WbsElementToHyperLinkConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var data = value as OrderInfo;
        if (data.OrderID % 2 == 0)
        {
            if (parameter.ToString() == "TextDecorations")
                return TextDecorations.Underline;
            else
                return new SolidColorBrush(Colors.Blue);
        }
        else
            return value;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

KB article - [How to display few cells of a columns have different foreground along with underline based on a condition in WPF DataGrid (SfDataGrid)?](https://www.syncfusion.com/kb/11887/how-to-display-few-cells-of-a-columns-have-different-foreground-along-with-underline-based)

## Requirements to run the demo
 Visual Studio 2015 and above versions
