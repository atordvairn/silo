<script>
  import { create } from "ipfs-http-client";
  const client = create("https://ipfs.infura.io:5001/api/v0");

  async function uploadFile() {
    var file = document.querySelector("#file")["files"][0];
    var reader = new FileReader();
    reader.onload = async function () {
      var added = await client.add(file);
      console.log(added);
    };
  }
</script>

<div class="navbar">silo</div>
<br />
<br />
<br />
<br />
<br />
<label class="labelForFile text-md p-2 " for="file"> chose a file </label>
<input type="file" name="file" id="file" on:change={uploadFile} />

<style global>
  * {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  .labelForFile {
    font-size: 20px;
    border-radius: 0.25rem;
	padding: 10px;
	background-color: rgb(248, 213, 170);
    box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  }

  input[type="file"] {
    display: none;
  }

  .navbar {
    display: flex;
    width: 100%;
    backdrop-filter: blur(2px);
    background-color: rgba(238, 238, 238, 0.623);
    position: fixed;
    font-size: 30px;
    padding: 10px;
    border-radius: 0.375rem;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
      0 2px 4px -1px rgba(0, 0, 0, 0.06);
    gap: 0.5rem;
  }
</style>
