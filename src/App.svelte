<script>
  import { create } from "ipfs-http-client";
  const client = create("https://ipfs.infura.io:5001/api/v0");

  let addr = "";
  let filename = "none";
  async function uploadFile() {
    addr = "#";
    var file = document.querySelector("#file")["files"][0];
    var reader = new FileReader();
    reader.onload = async function () {

      var added = await client.add(file);
      filename = file.name;
      addr = "https://infura-ipfs.io/ipfs/" + added.path;
    };
    reader.readAsDataURL(file);
  }
</script>

<div class="navbar">
  <div class="heading-nav">silo - store files on ipfs</div>
</div>
<br />
<br />
<br />
<br />
<br />
<label class="labelForFile text-md p-2 " for="file"> chose a file </label>
<input type="file" name="file" id="file" on:change={uploadFile} />
<br />
<div class="uploadText">
  <div style="margin: auto;">
      <a href={addr} target="_blank" rel="noopener noreferrer">
        {filename}
      </a>
  </div>
</div>

<style global>
  .uploadText {
    font-size: 20px;
    margin: 30px;
    word-wrap: normal;
    background: rgb(248, 213, 170);
    border-radius: 0.375rem;
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

  .heading-nav {
    margin: auto;
  }

  .navbar {
    /* margin-top: auto;
    margin-bottom: auto;*/
    display: flex;
    width: 100vw;
    backdrop-filter: blur(2px);
    background-color: rgba(238, 238, 238, 0.623);
    position: fixed;
    font-size: 30px;
    border-radius: 0.375rem;
    height: 4.5rem;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
      0 2px 4px -1px rgba(0, 0, 0, 0.06);
  }
</style>
