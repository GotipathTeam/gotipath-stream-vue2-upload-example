<template>
  <div>
    <Dashboard :uppy="uppy" />
  </div>
</template>

<script>
import AwsS3 from "@uppy/aws-s3";
import Uppy from "@uppy/core";
import { Dashboard } from "@uppy/vue";
import "@uppy/core/dist/style.css";
import "@uppy/dashboard/dist/style.css";
const uppy = new Uppy();

uppy.setOptions({
  debug: false,
  autoProceed: true,
  allowMultipleUploads: false,
  allowMultipleUploadBatches: true,
  proudlyDisplayPoweredByUppy: false,
});

const LibraryId = "35d44b32-fbc9-448a-ada4-96557f7cc13";
const ClientId = "92f9d000-5051-4339-9b3a-91f1c2a4c07";
const ApiKey =
  "8b6PNtL8Br0hvpa3R/UK6Nxxtkm7Clwa5WQGvPDdw99xTY2wkOLRQ9P9NQ0B8KkvgQ";

// AUTH HEADERS
const headers = {
  "X-Auth-ClientId": ClientId,
  "X-Auth-LibraryId": LibraryId,
  "X-Auth-ApiKey": ApiKey,
};

uppy.use(AwsS3, {
  shouldUseMultipart: true,
  companionUrl: "https://apistream.gotipath.com/v1/uploads/",
  companionHeaders: {
    "uppy-auth-token": JSON.stringify(headers),
  },
});

uppy.on("file-added", (file) => {
  uppy.setFileMeta(file.id, {
    video_id: "8b4d2ae2-63ec-4830-b506-19be1ee2d2c3",
    library_id: LibraryId,
    collection_id: "",
  });
});

export default {
  name: "uploader",
  components: {
    Dashboard,
  },
  data() {
    return {
      uppy,
    };
  },

  mounted() {
    console.log("mounted");
  },
};
</script>
