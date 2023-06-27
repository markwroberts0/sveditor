<script>
  import {
    Table,
    TableBody,
    TableBodyCell,
    TableBodyRow,
    TableHead,
    TableHeadCell,
    Indicator,
    Badge,
    Button,
    Toolbar,
    ToolbarButton,
    ToolbarGroup,
  } from "flowbite-svelte";

  import data from "../data/data.json";

  /**
   * Determines the color based on the status.
   * @param {string} status - The status of the item.
   */
  function getColor(status) {
    return status === "On Track"
      ? "green"
      : status === "At Risk"
      ? "yellow"
      : "red";
  }

  let searchTerm = "";
  $: filteredList = data;

  /**
   * Determines the color based on the status.
   * @param {string} name - The name of the item.
   */
  function filterOnName(name) {
    filteredList = data.filter((data) => data.name.indexOf(name) !== -1);
  }
  /**
   * Determines the color based on the status.
   * @param {string} directorate - The directorate of the item.
   */
  function filterOnDir(directorate) {
    filteredList = data.filter(
      (data) => data.directorate.indexOf(directorate) !== -1
    );
  }
  function resetFilters() {
    filteredList = data;
  }
</script>

<Table hoverable={true}>
  <caption
    class="p-5 text-lg font-semibold text-left text-gray-900 bg-white dark:text-white dark:bg-gray-800"
  >
    Objective status
    <Button dir="" class="right-0 mr-6" color="light" on:click={resetFilters}
      >Reset Filters</Button
    >
    <p class="mt-1 text-sm font-normal text-gray-500 dark:text-gray-400">
      Browse objective statuses by directorate and tagged with big plays.
    </p>
    <Toolbar>
      <ToolbarButton
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M2.25 12l8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25"
          /></svg
        ></ToolbarButton
      >
      <ToolbarButton
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M3.75 4.875c0-.621.504-1.125 1.125-1.125h4.5c.621 0 1.125.504 1.125 1.125v4.5c0 .621-.504 1.125-1.125 1.125h-4.5A1.125 1.125 0 013.75 9.375v-4.5zM3.75 14.625c0-.621.504-1.125 1.125-1.125h4.5c.621 0 1.125.504 1.125 1.125v4.5c0 .621-.504 1.125-1.125 1.125h-4.5a1.125 1.125 0 01-1.125-1.125v-4.5zM13.5 4.875c0-.621.504-1.125 1.125-1.125h4.5c.621 0 1.125.504 1.125 1.125v4.5c0 .621-.504 1.125-1.125 1.125h-4.5A1.125 1.125 0 0113.5 9.375v-4.5z"
          /><path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6.75 6.75h.75v.75h-.75v-.75zM6.75 16.5h.75v.75h-.75v-.75zM16.5 6.75h.75v.75h-.75v-.75zM13.5 13.5h.75v.75h-.75v-.75zM13.5 19.5h.75v.75h-.75v-.75zM19.5 13.5h.75v.75h-.75v-.75zM19.5 19.5h.75v.75h-.75v-.75zM16.5 16.5h.75v.75h-.75v-.75z"
          /></svg
        ></ToolbarButton
      >
      <ToolbarButton
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75"
          /></svg
        ></ToolbarButton
      >
    </Toolbar>
  </caption>
  <TableHead>
    <TableHeadCell>Directorate</TableHeadCell>
    <TableHeadCell>Name</TableHeadCell>
    <TableHeadCell>Big Play</TableHeadCell>
    <TableHeadCell>Status</TableHeadCell>
  </TableHead>
  <TableBody>
    {#each filteredList as item}
      <TableBodyRow>
        <TableBodyCell on:click={() => filterOnDir(item.directorate)}
          >{item.directorate}</TableBodyCell
        >
        <TableBodyCell on:click={() => filterOnName(item.name)}
          >{item.name}</TableBodyCell
        >
        <TableBodyCell>{item.bigplay}</TableBodyCell>
        <TableBodyCell>
          <Badge color={getColor(item.status)} rounded class="px-2.5 py-0.5">
            <Indicator
              color={getColor(item.status)}
              size="xs"
              class="mr-1"
            />{item.status}
          </Badge>
        </TableBodyCell>
      </TableBodyRow>
    {/each}
  </TableBody>
</Table>
