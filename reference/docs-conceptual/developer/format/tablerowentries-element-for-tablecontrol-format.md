---
description: TableRowEntries Element
ms.date: 08/25/2021
title: TableRowEntries Element
---
# TableRowEntries Element

Defines the rows of the table.

## Schema

- Configuration Element
- ViewDefinitions Element
- View Element
- TableControl Element
- TableRowEntries Element

## Syntax

```xml
<TableRowEntries>
  <TableRowEntry>...</TableRowEntry>
</TableRowEntries>
```

## Attributes and Elements

The following sections describe the attributes, child elements, and parent element of the
`TableRowEntries` element.

### Attributes

None.

### Child Elements

|Element|Description|
|-------------|-----------------|
|[TableRowEntry Element for TableRowEntries for TableControl](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)|Required element.<br /><br /> Defines the data that is displayed in a row of the table.|

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[TableControl Element](./tablecontrol-element-format.md)|Defines a table format for a view.|

## Remarks

You must specify one or more `TableRowEntry` elements for the table view. There is no maximum limit
to the number of `TableRowEntry` elements that can be added nor is their order significant.

For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).

## Example

The following example shows a `TableRowEntries` element that defines a row that displays the values
of two properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process)
object.

```xml
<TableRowEntries>
  <TableRowEntry>
    <EntrySelectedBy>
      <TypeName>System.Diagnostics.Process</TypeName>
    </EntrySelectedBy>
    <TableColumnItems>
      <TableColumnItem>
        <PropertyName> Property for first column</PropertyName>
      </TableColumnItem>
      <TableColumnItem>
        <PropertyName> Property for second column</PropertyName>
      </TableColumnItem>
    </TableColumnItems>
  </TableRowEntry>
</TableRowEntries>

```

## See Also

[Creating a Table View](./creating-a-table-view.md)

[TableControl Element](./tablecontrol-element-format.md)

[TableRowEntry Element](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
