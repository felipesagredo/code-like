<template>
  <div class="vscode">
    <div class="editor">
      <!-- Header -->
      <div class="header">
        <div class="button-opciones">
          <button @click="handleButtonClick">{{ showSidebar ? 'Ocultar menú' : 'Mostrar menú' }}</button>
        </div>
        <!-- Sidebar -->
        <div class="sidebar" v-if="showSidebar">
          <!-- Sidebar Content -->
          <ul>
            <li><a href="#">Nuevo</a></li>
            <li><input type="file" @change="handleFileSelect" accept=".txt"/></li>
            <li><button @click="saveFileContent">Guardar</button></li>
            <li><a href="#">Opciones</a></li>
            <li><a href="#">GitHub</a></li>
            <li><button @click="handleButtonClickNotas">{{ showNotas ? 'Ocultar Notas' : 'Mostrar Notas' }}</button></li>
          </ul>
        </div>
        
      </div>
      <!-- Editor Content -->
      <div class="editor-content">
        <pre><textarea v-model="fileContent" class="custom-textarea"></textarea></pre>
      </div>
    </div>
    <div class="selecciona-archivo" v-if="showNotas">
      <h2>Notas</h2>
      <h5>Escribe o sube tus notas...</h5>
      <input type="file" @change="handleFileSelectTarea" accept=".txt"/>
      <br/><br/>
      <textarea class="custom-textarea-tarea" v-model="fileContentTarea"></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VSCodeLike',
  methods: {
    saveFileContent() {
      // Verifica si hay contenido para guardar
      if (this.fileContent) {
        // Crea un nuevo objeto Blob con el contenido de fileContent
        const blob = new Blob([this.fileContent], { type: 'text/plain' });
        // Crea una URL para el Blob
        const url = window.URL.createObjectURL(blob);
        // Crea un enlace (link) para descargar el archivo
        const a = document.createElement('a');
        a.href = url;
        a.download = 'miarchivo.txt'; // Nombre del archivo a guardar
        // Simula un clic en el enlace para iniciar la descarga
        a.click();
        // Libera los recursos utilizados
        window.URL.revokeObjectURL(url);
      } else {
        // Muestra un mensaje de error o realiza alguna acción apropiada si no hay contenido para guardar.
        console.error('No hay contenido para guardar.');
      }
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
    toggleNotas() {
      this.showNotas = !this.showNotas;
    },
    handleButtonClick() {
      this.toggleSidebar();
    },
    handleButtonClickNotas() {
      this.toggleNotas();
    },
    handleFileSelect(event) {
      const file = event.target.files[0];
      if (file) {
        this.readFileContent(file);
      }
    },
    handleFileSelectTarea(event) {
      const file = event.target.files[0];
      if (file) {
        this.readFileContentTarea(file);
      }
    },
    async readFileContent(file) {
      try {
        const text = await this.readFileAsync(file);
        this.fileContent = text;
      } catch (error) {
        console.error('Error al cargar el archivo .txt', error);
      }
    },
    async readFileContentTarea(file) {
      try {
        const text = await this.readFileAsync(file);
        this.fileContentTarea = text;
      } catch (error) {
        console.error('Error al cargar el archivo .txt', error);
      }
    },
    readFileAsync(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = (event) => {
          resolve(event.target.result);
        };
        reader.onerror = (error) => {
          reject(error);
        };
        reader.readAsText(file);
      });
    },
  },
  data() {
    return {
      showSidebar: true,
      showNotas: true,
      fileContent: null,
      fileContentTarea: null,
    };
  },
  mounted() {
    // this.loadFileContent(); // Puedes eliminar esta línea, ya que no es necesaria aquí
  },
};
</script>

<style scoped>
.vscode {
  display: flex;
  justify-content: center;
  align-items: center;
  height: fit-content;
  background-color: #2f97d0;
  box-sizing: border-box;
  position: relative;
}
.editor {
  background-color: #333;
  color: #fff;
  display: flex;
  overflow: hidden;
  width: 100%;
  height: 100vh;
  position: relative;
}
.editor-content {
  flex: 1;
  padding: 0px;
  font-family: 'Monaco', monospace;
  white-space: pre;
}
.header {
  background-color: #444;
  padding: 0px;
  margin: 0px;
  text-align: left;
  font-size: 14px;
  box-sizing: border-box;
  position: relative;
  z-index: 100;
}
.button-opciones {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}
.sidebar {
  background-color: #2f2f5b;
  width: 850px;
  height: fit-content;
  top: 0px;
  left: 80px;
  z-index: 4;
  display: flex;
  padding: 0px;
  margin: 0px;
  position: absolute;
  box-sizing: border-box;
  vertical-align: middle;
}
ul {
  list-style: none;
  display: flex;
  top: 0px;
  width: 700px;
  padding: 0px;
  margin-top: 0px;
  margin-bottom: 0px;
  gap: 10px;
  text-align: center;
  box-sizing: border-box;
  position: absolute;
}
li {
  margin-top: 8px;
  gap: 5px;
}
li input[type="file"] {
    padding: 10px; /* Añade un relleno alrededor del input */
    border: 2px solid #ccc; /* Agrega un borde alrededor del input */
    border-radius: 5px; /* Añade bordes redondeados */
  }
a {
  color: #9cdcfe;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
.custom-textarea {
  position: relative;
  z-index: 1;
  top: 40px;
  padding: 20px;
  margin: 0px;
  width: 100%;
  height: 70vh;
  border: none;
  resize: none;
  outline: none;
  scrollbar-width: thin;
  scrollbar-color: #555 #1e1e1e;
  font-family: 'Monaco', monospace;
  color: #d4d4d4;
  background-color: #1e1e1e;
}
.custom-textarea-tarea{
  width: 300px;
  height: 300px;
  padding: 10px;
  resize: none;
  overflow: auto;
}
.selecciona-archivo {
  background-color: rgb(76, 144, 144);
  width: fit-content;
  height: fit-content;
  text-align: left;
  box-sizing: border-box;
  position: absolute;
  margin: 10px;
  padding: 10px;
  right: 10px;
  top: 0;
  z-index: 2;
  position: absolute;
}
h2{
  margin-top: 0;
  margin-bottom: 0;
}
.custom-textarea::-webkit-scrollbar {
  width: 8px;
}
.custom-textarea::-webkit-scrollbar-thumb {
  background: #555;
  border-radius: 4px;
}
.custom-textarea::-webkit-scrollbar-thumb:hover {
  background: #888;
}
.title {
  font-weight: bold;
}
</style>
