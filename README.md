[index.html](https://github.com/user-attachments/files/24547200/index.html)
<!DOCTYPE html>
<html lang="pt-pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tugaflix - Streaming</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>

    <div id="tela-perfis" class="container-principal">
        <h1 class="titulo-principal">Quem está a ver?</h1>
        <div id="lista-perfis" class="perfis-row">
            <div class="perfil-card" onclick="abrirModal()">
                <div class="avatar-box add-btn"><i class="fas fa-plus-circle"></i></div>
                <span class="perfil-nome">Novo Perfil</span>
            </div>
        </div>
    </div>

    <div id="modal-adicionar" class="modal-overlay">
        <div class="modal-box">
            <h2 class="modal-titulo">Adicionar Perfil</h2>
            <input type="text" id="nome-novo-perfil" placeholder="Nome do perfil">
            <div class="modal-actions">
                <button class="btn-guardar" onclick="salvarPerfil()">Guardar</button>
                <button class="btn-cancelar" onclick="fecharModal()">Sair</button>
            </div>
        </div>
    </div>

    <div id="tela-filmes" style="display: none;">
        <nav class="navbar">
            <h2 class="logo">TUGAFLIX</h2>
            <img id="avatar-sessao" src="" class="nav-avatar" onclick="location.reload()">
        </nav>
        <main class="main-content">
            <h3 class="row-title">Séries</h3>
            <div class="movie-list">
                <div class="movie-card" onclick="abrirSerie('miraculous', 10)">
                    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTia4CyMJ6uRjFyi9fqTHufIZX5GYC9-eXOUmoHb3OUGHSUUhEIWODAn2fXKWSZXk6RqGk6zFkiybqMcH8untLoGAuIMt_ccyF0RWlBXHBNeA&s=10">
                </div>
            </div>
        </main>
    </div>

    <div id="player-container" class="player-overlay" style="display: none;">
        <div class="controles-topo">
            <button class="btn-p-player" onclick="fecharVideoLocal()"><i class="fas fa-arrow-left"></i> Voltar</button>
            <button class="btn-p-player" onclick="toggleLista()"><i class="fas fa-list"></i> Episódios</button>
        </div>
        <div class="layout-player">
            <video id="video-local" controls onended="proximoEpisodio()"></video>
            <div id="painel-episodios" class="painel-episodios">
                <h3>Lista de Episódios</h3>
                <div id="lista-episodios-render"></div>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
[style.css](https://github.com/user-attachments/files/24547201/style.css)
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: #141414; color: white; font-family: Arial, sans-serif; overflow-x: hidden; }

/* PERFIS */
.container-principal { height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; }
.titulo-principal { font-size: 2.5rem; margin-bottom: 2rem; }
.perfis-row { display: flex; gap: 20px; flex-wrap: wrap; justify-content: center; }
.perfil-card { cursor: pointer; text-align: center; width: 150px; }
.avatar-box { width: 150px; height: 150px; background-size: cover; border-radius: 4px; border: 3px solid transparent; transition: 0.3s; }
.perfil-card:hover .avatar-box { border-color: white; transform: scale(1.05); }
.add-btn { display: flex; align-items: center; justify-content: center; font-size: 3rem; background: #333; color: #777; }

/* NAVBAR */
.navbar { padding: 15px 4%; display: flex; justify-content: space-between; background: black; position: fixed; width: 100%; top: 0; z-index: 500; }
.logo { color: #e50914; font-weight: bold; }
.nav-links { display: flex; list-style: none; gap: 15px; margin-left: 20px; }
.nav-avatar { width: 35px; border-radius: 4px; cursor: pointer; }

/* FILMES */
.main-content { padding: 100px 4% 20px; }
.movie-list { display: flex; gap: 10px; }
.movie-card { width: 200px; cursor: pointer; transition: 0.3s; }
.movie-card img { width: 100%; border-radius: 4px; }
.movie-card:hover { transform: scale(1.1); }

/* PLAYER E TELA CHEIA */
.player-overlay { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: black; z-index: 9999; }
.controles-topo { position: absolute; top: 20px; left: 20px; z-index: 10001; display: flex; gap: 10px; }
.btn-p-player { background: rgba(0,0,0,0.7); color: white; border: 1px solid #666; padding: 10px 15px; cursor: pointer; border-radius: 4px; }

.layout-player { display: flex; width: 100%; height: 100%; position: relative; }
#video-local { width: 100%; height: 100%; object-fit: contain; }

.painel-episodios { 
    position: absolute; right: -400px; top: 0; width: 350px; height: 100%; 
    background: rgba(20, 20, 20, 0.9); transition: 0.5s; padding: 80px 20px; 
    overflow-y: auto; border-left: 1px solid #333; 
}
.painel-episodios.visivel { right: 0; }

.card-ep { display: flex; align-items: center; gap: 10px; padding: 10px; cursor: pointer; border-bottom: 1px solid #222; }
.card-ep img { width: 80px; border-radius: 4px; }
.card-ep.ativo { border-left: 4px solid red; background: #222; }

/* MODAL */
.modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 2000; justify-content: center; align-items: center; }
.modal-box { background: #141414; padding: 30px; border-radius: 8px; width: 400px; }
#nome-novo-perfil { width: 100%; padding: 10px; margin: 10px 0; background: #444; color: white; border: none; }
.btn-guardar { background: white; color: black; padding: 10px 20px; border: none; cursor: pointer; font-weight: bold; }
[script.js](https://github.com/user-attachments/files/24547202/script.js)
