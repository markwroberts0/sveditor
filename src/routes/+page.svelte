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
