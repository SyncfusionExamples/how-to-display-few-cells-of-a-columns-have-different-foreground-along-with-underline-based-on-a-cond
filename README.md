# How to display few cells of a columns have different foreground along with underline based on a condition in WPF DataGrid (SfDataGrid)?

How to display few cells of a columns have different foreground along with underline based on a condition in WPF DataGrid (SfDataGrid)?
# About the sample

In SfDataGrid, you can display few cells of columns have different foreground along with underline based on conditions.

```xml
<Window.Resources>
    <local:WbsElementToHyperLinkConverter x:Key="WbsElementToHyperLinkConverter"/>
    <Style x:Key="SymbolCellStyle1" TargetType="syncfusion:GridCell">
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="syncfusion:GridCell">
                    <Border x:Name="PART_RowHeaderCellBorder"
                    BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}">
                        <!--RowIndex is displayed here -->
                        <TextBlock  Text="{Binding Path=OrderID}" 
                                            TextDecorations="{Binding Converter={StaticResource WbsElementToHyperLinkConverter},ConverterParameter=TextDecorations}" 
                                            Foreground="{Binding Converter={StaticResource WbsElementToHyperLinkConverter},ConverterParameter=ForeGround}" />
                    </Border>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</Window.Resources>

<syncfusion:GridTextColumn MappingName="OrderID" AllowFiltering="False" MinimumWidth="10" Width="90" >
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
## Requirements to run the demo
 Visual Studio 2015 and above versions
