# How to control button visibility on row selection in Flutter DataTable (SfDataGrid)?

In this article, we will show you how to control button visibility on row selection in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

To initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties, first create an instance of the [DataGridController](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridController-class.html) and assign it to the [controller](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/controller.html) property. Use the [selectedRows](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridController/selectedRows.html) list from the DataGridController to check if a row is selected. In the [buildRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/buildRow.html) method, if a row is selected, display an ElevatedButton; otherwise, show an empty widget (SizedBox.shrink()). When the button is clicked, it shows an AlertDialog with details of the selected row.

```dart
 @override
  DataGridRowAdapter? buildRow(DataGridRow row) {
    bool isSelected = controller.selectedRows.contains(row);
    return DataGridRowAdapter(
      cells:
          row.getCells().map<Widget>((dataGridCell) {
            return Container(
              alignment: Alignment.center,
              child:
                  dataGridCell.columnName == 'button'
                      ? LayoutBuilder(
                        builder: (
                          BuildContext context,
                          BoxConstraints constraints,
                        ) {
                          return isSelected
                              ? ElevatedButton(
                                onPressed: () {
                                  showDialog(
                                    context: context,
                                    builder:
                                        (context) => AlertDialog(
                                          content: SizedBox(
                                            height: 100,
                                            child: Column(
                                              mainAxisAlignment:
                                                  MainAxisAlignment
                                                      .spaceBetween,
                                              children: [
                                                Text(
                                                  'Employee ID: ${row.getCells()[0].value.toString()}',
                                                ),
                                                Text(
                                                  'Employee Name: ${row.getCells()[1].value.toString()}',
                                                ),
                                                Text(
                                                  'Employee Designation: ${row.getCells()[2].value.toString()}',
                                                ),
                                              ],
                                            ),
                                          ),
                                        ),
                                  );
                                },
                                child: const Text('Details'),
                              )
                              : const SizedBox.shrink();
                        },
                      )
                      : Text(dataGridCell.value.toString()),
            );
          }).toList(),
    );
}
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-control-button-visibility-on-row-selection-in-Flutter-DataTable).