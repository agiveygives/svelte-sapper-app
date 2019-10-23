<!--
  - Component: Table
  - Description: Render a table with customizable headers and data attributes
  - Props:
    * isLoading {bool} - tells the components whether the data is being fetched or not
    * errorCode {Integer} - The error code if the data fetch failed
    * headers {Array} - An Array of strings to render for the table headers
    * data {Array} - An Array of objects that contain the data for each row, data keys should match column headers.
-->

<script>
  export let isLoading = true;
  export let errorCode = null;
  export let headers = [];
  export let data = [];

  import DataTable, {Head, Body, Row, Cell} from '@smui/data-table';
</script>

{#if isLoading}
<!-- render table with loading icon -->
{:else if errorCode !== null}
<!-- render table with error icon/message -->
{:else if headers.length > 0}
  <DataTable table$aria-label="Generated Table">
    <Head>
      <Row>
        {#each headers as header}
          <Cell>{header}</Cell>
        {/each}
      </Row>
    </Head>
    <Body>
      {#if data.length > 0}
        {#each data as rowData}
          <Row>
            {#each headers as rowHeader}
              <Cell>{rowData[rowHeader] || '--'}</Cell>
            {/each}
          </Row>
        {/each}
      {:else}
        <Row>
          <Cell colspan={`${headers.length}`} align="center">
            no data
          </Cell>
        </Row>
      {/if}
    </Body>
  </DataTable>
{:else}
  <div></div>
{/if}
