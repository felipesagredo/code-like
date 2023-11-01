<template>
  <div class="vscode">
    <div class="editor">
      <!-- Header -->
      <div class="header">
        <div class="title">Code Like</div>
      </div>

      <!-- Editor Content -->
      <div class="editor-content">
        <pre><textarea v-model="code" class="custom-textarea"></textarea></pre>
      </div>

      <!-- Sidebar -->
      <div class="sidebar">
        <!-- Sidebar Content -->
        <ul>
          <li><a href="#">Nuevo archivo</a></li>
          <li><a href="#">Abrir proyecto</a></li>
          <li><a href="#">Opciones</a></li>
          <li><a href="#">Abrir GitHub</a></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VSCodeLike',
}
</script>

<style scoped>
.vscode {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.editor {
  background-color: #333;
  color: #fff;
  display: flex;
  border: 1px solid #555;
  border-radius: 4px;
  overflow: hidden;
  width: 600px;
  height: 60vh;
}

.editor-content {
  flex: 1;
  padding: 10px;
  font-family: 'Monaco', monospace;
  white-space: pre;
}

.custom-textarea {
  width: 94%;
  height: 50vh;
  background-color: #1e1e1e;
  color: #d4d4d4;
  font-family: 'Monaco', monospace;
  border: none;
  resize: none;
  outline: none;
  padding: 10px;  /* Personalizar la barra de desplazamiento */
  scrollbar-width: thin;
  scrollbar-color: #555 #1e1e1e;
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
.header {
  background-color: #444;
  padding: 8px;
  text-align: center;
  font-size: 18px;
}

.title {
  font-weight: bold;
}

.editor-content {
  flex: 1;
  padding: 10px;
  font-family: 'Monaco', monospace;
  white-space: pre;
}

.sidebar {
  background-color: #2d2d30;
  padding: 10px;
}

ul {
  list-style: none;
  padding: 0;
  text-align: left;
}

li {
  margin: 5px 0;
}

a {
  color: #9cdcfe;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
