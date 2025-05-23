There are several excellent libraries for rendering tables in web applications, especially for displaying leaderboard data with images. Here are some of the best options:

1. **React Table**:
   - A lightweight and flexible library for building tables in React applications.
   - Supports custom cell rendering, which allows you to easily include images in your table cells.
   - Highly customizable and can handle large datasets efficiently.

2. **AG Grid**:
   - A powerful grid component for frameworks like React, Angular, and Vue.
   - Supports complex features like sorting, filtering, and pagination.
   - You can easily render images in cells and customize the appearance of the grid.

3. **DataTables**:
   - A jQuery plugin that provides advanced interaction controls for HTML tables.
   - Supports features like pagination, sorting, and filtering.
   - You can include images in table cells using custom rendering functions.

4. **Tabulator**:
   - A feature-rich JavaScript table library that is easy to use and highly customizable.
   - Supports rendering images, custom cell formatting, and various data types.
   - Offers built-in support for sorting, filtering, and pagination.

5. **Handsontable**:
   - A JavaScript data grid component that provides a spreadsheet-like experience.
   - Supports custom cell rendering, allowing you to display images alongside text.
   - Good for applications that require inline editing and complex data manipulation.

### Example of Using React Table with Images

If you choose to use React Table, here's a simple example of how you might render a leaderboard with user avatars:

```jsx
import React from 'react';
import { useTable } from 'react-table';

const Leaderboard = ({ data }) => {
  const columns = React.useMemo(
    () => [
      {
        Header: 'Rank',
        accessor: 'rank', // accessor is the "key" in the data
      },
      {
        Header: 'User ',
        accessor: 'user',
      },
      {
        Header: 'Avatar',
        accessor: 'avatar',
        Cell: ({ cell: { value } }) => <img src={value} alt="User  Avatar" style={{ width: '50px', height: '50px' }} />,
      },
    ],
    []
  );

  const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } = useTable({ columns, data });

  return (
    <table {...getTableProps()}>
      <thead>
        {headerGroups.map(headerGroup => (
          <tr {...headerGroup.getHeaderGroupProps()}>
            {headerGroup.headers.map(column => (
              <th {...column.getHeaderProps()}>{column.render('Header')}</th>
            ))}
          </tr>
        ))}
      </thead>
      <tbody {...getTableBodyProps()}>
        {rows.map(row => {
          prepareRow(row);
          return (
            <tr {...row.getRowProps()}>
              {row.cells.map(cell => (
                <td {...cell.getCellProps()}>{cell.render('Cell')}</td>
              ))}
            </tr>
          );
        })}
      </tbody>
    </table>
  );
};

export default Leaderboard;
```

### Conclusion

Choose a library based on your specific needs, such as the framework you are using, the complexity of the data, and the features you require. Each of these libraries has its strengths, so consider experimenting with a few to see which one fits your project best.