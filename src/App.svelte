<script>
  import { create } from "ipfs-http-client";
  import Swal from "sweetalert2";
  const client = create("https://ipfs.infura.io:5001/api/v0");

  let addr;
  let filename;
  let uploading;

  async function uploadFile() {
    var file = document.querySelector("#file")["files"][0];
    var reader = new FileReader();
    reader.onload = async function () {
      uploading = true;
      addr = "#";
      filename = "uploading...";
      var added = await client.add(file);
      filename = file.name;
      uploading = false;
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
{#if uploading == false}
  <div class="uploadText">
    <div style="margin: auto;">
      your file: <a href={addr} target="_blank" rel="noopener noreferrer">
        {filename}
      </a>
      <br />
      <div style="margin: 20px;">
        <div
          class="labelForFile"
          on:click={() => {
            navigator.clipboard.writeText(addr).then(() => {
              let toast = Swal.mixin({
                toast: true,
                position: "bottom-end",
                timer: 1000,
                timerProgressBar: true,
              });

              toast.fire({
                title: "copied",
                timer: 1000,
                icon: "success",
                showConfirmButton: false,
              });
            });
          }}
        >
          copy link to clipboard
        </div>
      </div>
    </div>
  </div>
{:else if uploading == true}
  <div class="uploadText">
    <div style="margin: auto;">uploading...</div>
  </div>
{/if}
<article>
  IPFS allows users to host and receive content in a manner similar to
  BitTorrent. As opposed to a centrally located server, IPFS is built around a
  decentralized system of user-operators who hold a portion of the overall data,
  creating a resilient system of file storage and sharing.
  <p>
    Any user in the network can serve a file by its content address, and other
    peers in the network can find and request that content from any node who has
    it using a distributed hash table.
  </p>
  In contrast to BitTorrent, IPFS aims to create a single global network. This means
  that if two users publish a block of data with the same hash, the peers downloading
  the content from "user 1" will also exchange data with the ones downloading it
  from "user 2". IPFS aims to replace protocols used for static webpage delivery
  by using gateways which are accessible with HTTP.Users may choose not to install
  an IPFS client on their device and instead use a public gateway. A list of these
  gateways is maintained on the IPFS GitHub page.

  <div class="labelForFile" style="width: 214px;margin-top: 10px;">
    <a
      class="a"
      href={"https://en.wikipedia.org/wiki/InterPlanetary_File_System"}
      target="_blank"
      rel="noopener noreferrer"
    >
      read more on wikipedia
    </a>
  </div>
</article>

<style global>
  body,
  html {
    margin: 0px !important;
    padding: 0px !important;
  }

  .a {
    text-decoration: none;

    color: inherit;
  }

  article {
    margin: 10px;
    margin-top: 100px;
    font-size: large;
  }

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
    cursor: pointer;
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
    width: 96vw;
    margin-right: 10px;
    backdrop-filter: blur(2px);
    background-color: rgba(238, 238, 238, 0.329);
    position: fixed;
    font-size: 1.3rem;
    border-radius: 0.375rem;
    height: 4.5rem;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
      0 2px 4px -1px rgba(0, 0, 0, 0.06);
  }
</style>
