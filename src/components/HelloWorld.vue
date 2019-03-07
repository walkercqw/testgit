<template>
  <div class="hello">
    <div id="files">点击上传</div>
  </div>  
</template>

<script>
import plupload from "plupload"
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      uploader:{},
    }
  },
  mounted(){
    this.uploadFiles()
  },
  methods:{
    uploadFiles(){
      this.uploader = new plupload.Uploader({
        browse_button:"files",
        filters:{
          mime_types:[
            {
              title:"Image files",
              extensions:"jpg,gif,png"
            }
          ],
          max_file_size:"400kb", //最大只能上传400kb的文件
          prevent_duplicates:true //不允许选取重复文件
        }
      });
      this.uploader.init();
      this.uploader.bind("FilesAdded",(up,files) => {
        console.log("文件添加到上传队列")
      }),
      this.uploader.bind("BeforeUpload",(up, file) => {
        console.log("文件准备上传")
      }),
      this.uploader.bind("UploadProgress",(up,file) => {
        console.log("文件正在上传中")
      }),
      this.uploader.bind("FileUploaded",(up,file,res) => {
        console.log("文件上传完成")
      })
      this.uploader.bind("Error",(code,file,message) => {
        console.log("文件上传错误")
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
.hello{
  #files{
    cursor: pointer;
  }
}
</style>
