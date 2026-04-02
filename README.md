# impress-es-relat-rios
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle de Impressões - Colégio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1800px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            padding: 20px;
        }

        header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .sync-status {
            background: rgba(255,255,255,0.2);
            color: white;
            padding: 10px 20px;
            border-radius: 20px;
            display: inline-block;
            margin-top: 10px;
            font-size: 0.9em;
        }

        .sync-status.online {
            background: #27ae60;
        }

        .sync-status.offline {
            background: #e74c3c;
        }

        .quota-warning {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            text-align: center;
            font-weight: bold;
            display: none;
            animation: pulse 2s infinite;
        }

        .quota-warning.show {
            display: block;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            transition: transform 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-card.quota {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
        }

        .stat-card.quota.warning {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            animation: pulse 2s infinite;
        }

        .stat-card h3 {
            color: #667eea;
            font-size: 2.2em;
            margin-bottom: 8px;
        }

        .stat-card.quota h3 {
            color: white;
        }

        .stat-card p {
            color: #666;
            font-weight: 600;
            font-size: 1.1em;
        }

        .stat-card.quota p {
            color: white;
        }

        .progress-bar {
            width: 100%;
            height: 12px;
            background: rgba(255,255,255,0.3);
            border-radius: 6px;
            margin-top: 10px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: white;
            border-radius: 6px;
            transition: width 0.5s ease;
        }

        .main-content {
            display: grid;
            grid-template-columns: 450px 1fr;
            gap: 30px;
        }

        @media (max-width: 1200px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }

        .form-section, .table-section {
            background: white;
            border-radius: 20px;
            padding: 35px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
        }

        .form-section h2, .table-section h2 {
            color: #333;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 3px solid #667eea;
            font-size: 1.5em;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            color: #555;
            font-weight: 600;
            font-size: 1.05em;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            padding: 14px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .form-group input:focus,
        .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .turma-info {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            margin-top: 15px;
            border: 2px solid #e9ecef;
        }

        .turma-row {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 15px;
        }

        .turma-row .form-group {
            margin-bottom: 0;
        }

        .turma-row label {
            font-size: 0.95em;
            margin-bottom: 8px;
        }

        .turma-row input,
        .turma-row select {
            padding: 12px;
            font-size: 15px;
        }

        .checkbox-group {
            display: flex;
            gap: 30px;
            flex-wrap: wrap;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .checkbox-item input[type="radio"] {
            width: 22px;
            height: 22px;
            cursor: pointer;
        }

        .checkbox-item label {
            margin: 0;
            font-weight: 500;
            cursor: pointer;
        }

        .btn {
            padding: 14px 30px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            width: 100%;
            padding: 16px;
            font-size: 1.1em;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-danger {
            background: #e74c3c;
            color: white;
            padding: 10px 18px;
            font-size: 14px;
        }

        .btn-danger:hover {
            background: #c0392b;
        }

        .btn-success {
            background: #27ae60;
            color: white;
            padding: 10px 18px;
            font-size: 14px;
        }

        .btn-success:hover {
            background: #219a52;
        }

        .filters {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .filters select {
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
        }

        .table-container {
            overflow-x: auto;
            border-radius: 10px;
            border: 1px solid #e0e0e0;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.95em;
        }

        th, td {
            padding: 14px 12px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        th {
            background: #667eea;
            color: white;
            font-weight: 600;
            position: sticky;
            top: 0;
            white-space: nowrap;
        }

        td {
            white-space: nowrap;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .badge {
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            white-space: nowrap;
        }

        .badge-a3 { background: #ffeaa7; color: #d63031; }
        .badge-a4 { background: #74b9ff; color: #0984e3; }
        .badge-color { background: #fd79a8; color: #e84393; }
        .badge-bw { background: #dfe6e9; color: #636e72; }
        .badge-frente-verso { background: #55efc4; color: #00b894; }
        .badge-frente { background: #fab1a0; color: #e17055; }
        .badge-av { background: #a29bfe; color: #6c5ce7; }
        .badge-cont { background: #74b9ff; color: #0984e3; }
        .badge-cad { background: #fd79a8; color: #e84393; }

        .actions {
            display: flex;
            gap: 8px;
        }

        .empty-state {
            text-align: center;
            padding: 60px 40px;
            color: #999;
        }

        .empty-state svg {
            width: 100px;
            height: 100px;
            margin-bottom: 20px;
            opacity: 0.5;
        }

        .export-btn {
            margin-bottom: 25px;
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .date-range {
            display: flex;
            gap: 12px;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }

        .date-range input {
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            padding: 35px;
            border-radius: 20px;
            max-width: 600px;
            width: 90%;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        .close-btn {
            font-size: 32px;
            cursor: pointer;
            color: #999;
        }

        .close-btn:hover {
            color: #333;
        }

        .room-summary {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 12px;
            margin-top: 25px;
            border: 1px solid #e9ecef;
        }

        .room-summary h4 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.2em;
        }

        .room-list {
            list-style: none;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 10px;
        }

        .room-list li {
            padding: 12px 15px;
            display: flex;
            justify-content: space-between;
            background: white;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 18px 28px;
            background: #27ae60;
            color: white;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.2);
            display: none;
            animation: slideInRight 0.3s ease;
            z-index: 2000;
            font-size: 1.05em;
        }

        @keyframes slideInRight {
            from {
                transform: translateX(100%);
            }
            to {
                transform: translateX(0);
            }
        }

        .notification.error {
            background: #e74c3c;
        }

        .notification.show {
            display: block;
        }

        .hidden {
            display: none !important;
        }
    </style>
<base target="_blank">
</head>
<body>
    <div class="container">
        <header>
            <h1>🖨️ Controle de Impressões</h1>
            <p>Sistema de Gerenciamento de Impressões do Colégio</p>
            <div id="syncStatus" class="sync-status offline">
                🔄 Conectando ao servidor...
            </div>
        </header>

        <div id="quotaWarning" class="quota-warning">
            ⚠️ ATENÇÃO: Cota mensal estourada! Você ultrapassou 20.000 impressões este mês.
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <h3 id="totalImpressoes">0</h3>
                <p>Total de Impressões</p>
            </div>
            <div class="stat-card">
                <h3 id="totalFolhas">0</h3>
                <p>Total de Folhas</p>
            </div>
            <div class="stat-card">
                <h3 id="totalCopias">0</h3>
                <p>Total de Cópias</p>
            </div>
            <div class="stat-card">
                <h3 id="impressoesHoje">0</h3>
                <p>Impressões Hoje</p>
            </div>
            <div class="stat-card quota" id="quotaCard">
                <h3 id="quotaRestante">20.000</h3>
                <p>Cota Mensal Restante</p>
                <div class="progress-bar">
                    <div class="progress-fill" id="quotaProgress" style="width: 100%"></div>
                </div>
            </div>
        </div>

        <div class="main-content">
            <div class="form-section">
                <h2>📄 Nova Impressão</h2>
                <form id="impressaoForm">

                    <div class="form-group">
                        <label for="dataImpressao">Data da Impressão</label>
                        <input type="date" id="dataImpressao" required>
                    </div>

                    <div class="form-group">
                        <label for="tipo">Tipo</label>
                        <select id="tipo" required>
                            <option value="">Selecione o tipo</option>
                            <option value="Av. conteúdo">Av. conteúdo</option>
                            <option value="Conteúdo">Conteúdo</option>
                            <option value="Caderno Atividades">Caderno Atividades</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="sala">Sala/Turma</label>
                        <select id="sala" required onchange="atualizarTurmaInfo()">
                            <option value="">Selecione a turma</option>
                            <option value="Infantil 4">Infantil 4</option>
                            <option value="Infantil 5">Infantil 5</option>
                            <option value="1ºAno">1ºAno</option>
                            <option value="2ºAno">2ºAno</option>
                            <option value="3ºAno">3ºAno</option>
                            <option value="4ºAno">4ºAno</option>
                            <option value="5ºAno">5ºAno</option>
                            <option value="6ºAno">6ºAno</option>
                            <option value="7ºAno">7ºAno</option>
                            <option value="8ºAno">8ºAno</option>
                            <option value="9ºAno">9ºAno</option>
                            <option value="1ª Série">1ª Série</option>
                            <option value="2ª Série">2ª Série</option>
                            <option value="3ª Série">3ª Série</option>
                        </select>
                    </div>

                    <div id="turmaInfo" class="turma-info hidden">
                        <div class="turma-row">
                            <div class="form-group">
                                <label for="turmaLetra">Turma (Letra)</label>
                                <select id="turmaLetra" required onchange="calcularCopias()">
                                    <option value="">Selecione</option>
                                    <option value="A">Turma A</option>
                                    <option value="B">Turma B</option>
                                    <option value="C">Turma C</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="quantidadeAlunos">Qtd. de Alunos</label>
                                <input type="number" id="quantidadeAlunos" min="1" required onchange="calcularCopias()" placeholder="Ex: 25">
                            </div>
                            <div class="form-group">
                                <label for="copiasCalculadas">Total de Cópias</label>
                                <input type="number" id="copiasCalculadas" min="1" readonly style="background: #e8e8e8; font-weight: bold;">
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="arquivo">Descrição do Conteúdo</label>
                        <input type="text" id="arquivo" required placeholder="Ex: Ciências - Ciclo da água, Matemática - Frações">
                    </div>

                    <div class="form-group">
                        <label for="impressora">Impressora Utilizada</label>
                        <select id="impressora" required>
                            <option value="">Selecione a impressora</option>
                            <option value="Konica Minolta C458">Konica Minolta C458</option>
                            <option value="Konica Minolta C458e">Konica Minolta C458e</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="operador">Operador Responsável</label>
                        <select id="operador" required>
                            <option value="">Selecione o operador</option>
                            <option value="Nicolas">Nicolas (Coordenador de Produção)</option>
                            <option value="Kayalane">Kayalane</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label>Formato da Folha</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="radio" name="formato" id="a4" value="A4" checked>
                                <label for="a4">A4</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="radio" name="formato" id="a3" value="A3">
                                <label for="a3">A3</label>
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label>Tipo de Impressão</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="radio" name="tipoImpressao" id="pb" value="Preto e Branco" checked>
                                <label for="pb">Preto e Branco</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="radio" name="tipoImpressao" id="colorido" value="Colorido">
                                <label for="colorido">Colorido</label>
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label>Frente e Verso</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="radio" name="frenteVerso" id="fv" value="Frente e Verso" checked>
                                <label for="fv">Sim (Frente e Verso)</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="radio" name="frenteVerso" id="frente" value="Frente apenas">
                                <label for="frente">Não (Apenas Frente)</label>
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="folhas">Quantidade de Folhas por Arquivo</label>
                        <input type="number" id="folhas" min="1" required placeholder="Número de folhas do documento">
                    </div>

                    <div class="form-group">
                        <label for="observacoes">Observações (Opcional)</label>
                        <input type="text" id="observacoes" placeholder="Alguma observação especial sobre esta impressão">
                    </div>

                    <button type="submit" class="btn btn-primary">➕ Registrar Impressão</button>
                </form>
            </div>

            <div class="table-section">
                <h2>📊 Histórico de Impressões</h2>

                <div class="date-range">
                    <label style="font-weight: 600; color: #555;">Filtrar por período:</label>
                    <input type="date" id="dataInicio">
                    <span style="color: #666;">até</span>
                    <input type="date" id="dataFim">
                    <button class="btn btn-success" onclick="filtrarPorData()">Filtrar</button>
                    <button class="btn" style="background: #95a5a6; color: white;" onclick="limparFiltro()">Limpar</button>
                </div>

                <div class="filters">
                    <select id="filtroOperador" onchange="filtrarTabela()">
                        <option value="">Todos os Operadores</option>
                        <option value="Nicolas">Nicolas</option>
                        <option value="Kayalane">Kayalane</option>
                    </select>
                    <select id="filtroImpressora" onchange="filtrarTabela()">
                        <option value="">Todas as Impressoras</option>
                        <option value="Konica Minolta C458">Konica Minolta C458</option>
                        <option value="Konica Minolta C458e">Konica Minolta C458e</option>
                    </select>
                    <select id="filtroTipo" onchange="filtrarTabela()">
                        <option value="">Todos os Tipos</option>
                        <option value="Av. conteúdo">Av. conteúdo</option>
                        <option value="Conteúdo">Conteúdo</option>
                        <option value="Caderno Atividades">Caderno Atividades</option>
                    </select>
                    <select id="filtroSala" onchange="filtrarTabela()">
                        <option value="">Todas as Turmas</option>
                    </select>
                </div>

                <div class="export-btn">
                    <button class="btn btn-success" onclick="exportarCSV()">📥 Exportar CSV</button>
                    <button class="btn btn-success" onclick="exportarPDF()">📄 Exportar PDF</button>
                    <button class="btn btn-danger" onclick="limparTudo()">🗑️ Limpar Todos os Dados</button>
                </div>

                <div class="table-container">
                    <table id="tabelaImpressoes">
                        <thead>
                            <tr>
                                <th>Data</th>
                                <th>Tipo</th>
                                <th>Turma</th>
                                <th>Descrição</th>
                                <th>Impressora</th>
                                <th>Operador</th>
                                <th>Formato</th>
                                <th>Cor</th>
                                <th>F/V</th>
                                <th>Folhas</th>
                                <th>Cópias</th>
                                <th>Total</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody id="corpoTabela">
                        </tbody>
                    </table>
                    <div id="emptyState" class="empty-state" style="display: none;">
                        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                        </svg>
                        <p>Nenhuma impressão registrada ainda</p>
                    </div>
                </div>

                <div class="room-summary">
                    <h4>📈 Resumo por Turma (Cópias Totais)</h4>
                    <ul id="resumoSalas" class="room-list">
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <div id="notification" class="notification"></div>

    <div id="editModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Editar Impressão</h2>
                <span class="close-btn" onclick="fecharModal()">&times;</span>
            </div>
            <form id="editForm">
                <input type="hidden" id="editId">
                <div class="form-group">
                    <label>Data</label>
                    <input type="date" id="editData" required>
                </div>
                <div class="form-group">
                    <label>Tipo</label>
                    <select id="editTipo" required>
                        <option value="Av. conteúdo">Av. conteúdo</option>
                        <option value="Conteúdo">Conteúdo</option>
                        <option value="Caderno Atividades">Caderno Atividades</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Turma Completa</label>
                    <input type="text" id="editSala" required>
                </div>
                <div class="form-group">
                    <label>Descrição</label>
                    <input type="text" id="editArquivo" required>
                </div>
                <div class="form-group">
                    <label>Folhas</label>
                    <input type="number" id="editFolhas" min="1" required>
                </div>
                <div class="form-group">
                    <label>Cópias</label>
                    <input type="number" id="editCopias" min="1" required>
                </div>
                <button type="submit" class="btn btn-primary">Salvar Alterações</button>
            </form>
        </div>
    </div>

    <script type="module">
        // Importar Firebase via CDN (ES6 modules)
        import { initializeApp } from 'https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js';
        import { 
            getFirestore, 
            collection, 
            addDoc, 
            doc, 
            getDoc, 
            getDocs, 
            updateDoc, 
            deleteDoc,
            onSnapshot,
            query,
            orderBy,
            serverTimestamp,
            setDoc
        } from 'https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js';

        // Configuração do Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyAJqNohimaiBIxZrWAZwTrzVgOTidNmJXI",
            authDomain: "srtgjjnhwsvhwt-wetyw-e-ryweywe.firebaseapp.com",
            projectId: "srtgjjnhwsvhwt-wetyw-e-ryweywe",
            storageBucket: "srtgjjnhwsvhwt-wetyw-e-ryweywe.firebasestorage.app",
            messagingSenderId: "757604431742",
            appId: "1:757604431742:web:3c9f1852e55e816cae652f"
        };

        // Inicializar Firebase
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        // Configurações
        const COTA_MENSAL = 20000;
        const COLLECTION_NAME = 'impressoes';
        const CONFIG_COLLECTION = 'config';

        // Estado global
        let impressoes = [];
        let quotaUsada = 0;
        let unsubscribe = null;

        // Elementos DOM
        const form = document.getElementById('impressaoForm');
        const corpoTabela = document.getElementById('corpoTabela');
        const emptyState = document.getElementById('emptyState');
        const notification = document.getElementById('notification');
        const turmaInfo = document.getElementById('turmaInfo');
        const syncStatus = document.getElementById('syncStatus');

        // Inicialização
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('dataImpressao').value = new Date().toISOString().split('T')[0];

            iniciarListener();
            carregarQuota();

            const hoje = new Date().toISOString().split('T')[0];
            document.getElementById('dataInicio').value = hoje;
            document.getElementById('dataFim').value = hoje;
        });

        // Listener em tempo real do Firestore
        function iniciarListener() {
            const q = query(collection(db, COLLECTION_NAME), orderBy('dataObj', 'desc'));

            unsubscribe = onSnapshot(q, (snapshot) => {
                impressoes = [];
                snapshot.forEach((doc) => {
                    impressoes.push({ id: doc.id, ...doc.data() });
                });

                atualizarTabela();
                atualizarEstatisticas();
                atualizarFiltroSalas();
                atualizarSyncStatus(true);
            }, (error) => {
                console.error('Erro ao sincronizar:', error);
                atualizarSyncStatus(false);
                showNotification('Erro de conexão. Verifique sua internet.', 'error');
            });
        }

        function atualizarSyncStatus(online) {
            if (online) {
                syncStatus.textContent = '🟢 Sincronizado em tempo real';
                syncStatus.className = 'sync-status online';
            } else {
                syncStatus.textContent = '🔴 Desconectado';
                syncStatus.className = 'sync-status offline';
            }
        }

        // Carregar quota do Firestore
        async function carregarQuota() {
            try {
                const docRef = doc(db, CONFIG_COLLECTION, 'quota_' + getMesAno());
                const docSnap = await getDoc(docRef);

                if (docSnap.exists()) {
                    quotaUsada = docSnap.data().usada || 0;
                } else {
                    quotaUsada = 0;
                    await salvarQuota();
                }
                atualizarQuota();
            } catch (error) {
                console.error('Erro ao carregar quota:', error);
            }
        }

        async function salvarQuota() {
            try {
                const docRef = doc(db, CONFIG_COLLECTION, 'quota_' + getMesAno());
                await setDoc(docRef, { usada: quotaUsada });
            } catch (error) {
                console.error('Erro ao salvar quota:', error);
            }
        }

        // Funções de Turma
        window.atualizarTurmaInfo = function() {
            const sala = document.getElementById('sala').value;
            if (sala) {
                turmaInfo.classList.remove('hidden');
                document.getElementById('turmaLetra').value = '';
                document.getElementById('quantidadeAlunos').value = '';
                document.getElementById('copiasCalculadas').value = '';
            } else {
                turmaInfo.classList.add('hidden');
            }
        };

        window.calcularCopias = function() {
            const turma = document.getElementById('turmaLetra').value;
            const alunos = parseInt(document.getElementById('quantidadeAlunos').value) || 0;

            if (turma && alunos > 0) {
                document.getElementById('copiasCalculadas').value = alunos;
            }
        };

        // Formulário
        form.addEventListener('submit', async function(e) {
            e.preventDefault();

            const sala = document.getElementById('sala').value;
            const turmaLetra = document.getElementById('turmaLetra').value;
            const salaCompleta = sala + (turmaLetra ? ' ' + turmaLetra : '');
            const copias = parseInt(document.getElementById('copiasCalculadas').value) || 1;
            const folhas = parseInt(document.getElementById('folhas').value) || 1;
            const totalImpressao = folhas * copias;

            if (quotaUsada + totalImpressao > COTA_MENSAL) {
                if (!confirm(`⚠️ ATENÇÃO: Esta impressão ultrapassará a cota mensal de ${COTA_MENSAL.toLocaleString()} impressões.\n\nCota usada: ${quotaUsada.toLocaleString()}\nEsta impressão: ${totalImpressao.toLocaleString()}\nTotal após impressão: ${(quotaUsada + totalImpressao).toLocaleString()}\n\nDeseja continuar mesmo assim?`)) {
                    return;
                }
            }

            const dataImpressao = document.getElementById('dataImpressao').value;
            const dataHora = new Date(dataImpressao + 'T' + new Date().toTimeString().split(' ')[0]);

            const novaImpressao = {
                data: new Date(dataImpressao).toLocaleDateString('pt-BR'),
                dataObj: dataHora.toISOString(),
                dataImpressao: dataImpressao,
                timestamp: serverTimestamp(),
                tipo: document.getElementById('tipo').value,
                sala: salaCompleta,
                turmaBase: sala,
                turmaLetra: turmaLetra,
                quantidadeAlunos: parseInt(document.getElementById('quantidadeAlunos').value) || 0,
                arquivo: document.getElementById('arquivo').value,
                impressora: document.getElementById('impressora').value,
                operador: document.getElementById('operador').value,
                formato: document.querySelector('input[name="formato"]:checked').value,
                tipoImpressao: document.querySelector('input[name="tipoImpressao"]:checked').value,
                frenteVerso: document.querySelector('input[name="frenteVerso"]:checked').value,
                folhas: folhas,
                copias: copias,
                observacoes: document.getElementById('observacoes').value
            };

            try {
                await addDoc(collection(db, COLLECTION_NAME), novaImpressao);

                quotaUsada += totalImpressao;
                await salvarQuota();
                atualizarQuota();

                form.reset();
                turmaInfo.classList.add('hidden');
                document.getElementById('dataImpressao').value = new Date().toISOString().split('T')[0];

                showNotification('Impressão registrada com sucesso!');
            } catch (error) {
                console.error('Erro ao salvar:', error);
                showNotification('Erro ao salvar impressão. Tente novamente.', 'error');
            }
        });

        // Funções de atualização
        function atualizarTabela(dados = impressoes) {
            corpoTabela.innerHTML = '';

            if (dados.length === 0) {
                emptyState.style.display = 'block';
                return;
            }

            emptyState.style.display = 'none';

            dados.forEach(imp => {
                const total = imp.folhas * imp.copias;
                let badgeTipo = 'badge-cont';
                if (imp.tipo === 'Av. conteúdo') badgeTipo = 'badge-av';
                if (imp.tipo === 'Caderno Atividades') badgeTipo = 'badge-cad';

                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${imp.data}</td>
                    <td><span class="badge ${badgeTipo}">${imp.tipo}</span></td>
                    <td>${imp.sala}</td>
                    <td>${imp.arquivo}</td>
                    <td>${imp.impressora}</td>
                    <td>${imp.operador}</td>
                    <td><span class="badge badge-${imp.formato.toLowerCase()}">${imp.formato}</span></td>
                    <td><span class="badge ${imp.tipoImpressao === 'Colorido' ? 'badge-color' : 'badge-bw'}">${imp.tipoImpressao}</span></td>
                    <td><span class="badge ${imp.frenteVerso === 'Frente e Verso' ? 'badge-frente-verso' : 'badge-frente'}">${imp.frenteVerso === 'Frente e Verso' ? 'F/V' : 'F'}</span></td>
                    <td>${imp.folhas}</td>
                    <td>${imp.copias}</td>
                    <td><strong>${total}</strong></td>
                    <td class="actions">
                        <button class="btn btn-success" onclick="editarImpressao('${imp.id}')">✏️</button>
                        <button class="btn btn-danger" onclick="excluirImpressao('${imp.id}')">🗑️</button>
                    </td>
                `;
                corpoTabela.appendChild(row);
            });

            atualizarResumoSalas(dados);
        }

        function atualizarEstatisticas() {
            const totalImpressoes = impressoes.length;
            const totalFolhas = impressoes.reduce((acc, imp) => acc + (imp.folhas * imp.copias), 0);
            const totalCopias = impressoes.reduce((acc, imp) => acc + imp.copias, 0);

            const hoje = new Date().toDateString();
            const impressoesHoje = impressoes.filter(imp => 
                new Date(imp.dataObj).toDateString() === hoje
            ).length;

            document.getElementById('totalImpressoes').textContent = totalImpressoes;
            document.getElementById('totalFolhas').textContent = totalFolhas.toLocaleString();
            document.getElementById('totalCopias').textContent = totalCopias.toLocaleString();
            document.getElementById('impressoesHoje').textContent = impressoesHoje;
        }

        function atualizarQuota() {
            const restante = Math.max(0, COTA_MENSAL - quotaUsada);
            const percentual = Math.max(0, (restante / COTA_MENSAL) * 100);

            document.getElementById('quotaRestante').textContent = restante.toLocaleString();
            document.getElementById('quotaProgress').style.width = percentual + '%';

            const quotaCard = document.getElementById('quotaCard');
            const quotaWarning = document.getElementById('quotaWarning');

            if (quotaUsada > COTA_MENSAL) {
                quotaCard.classList.add('warning');
                quotaWarning.classList.add('show');
                document.getElementById('quotaRestante').textContent = '-' + (quotaUsada - COTA_MENSAL).toLocaleString();
            } else {
                quotaCard.classList.remove('warning');
                quotaWarning.classList.remove('show');
            }
        }

        function atualizarResumoSalas(dados = impressoes) {
            const resumo = {};
            dados.forEach(imp => {
                if (!resumo[imp.sala]) {
                    resumo[imp.sala] = 0;
                }
                resumo[imp.sala] += imp.copias;
            });

            const lista = document.getElementById('resumoSalas');
            lista.innerHTML = '';

            Object.entries(resumo)
                .sort((a, b) => b[1] - a[1])
                .forEach(([sala, copias]) => {
                    const li = document.createElement('li');
                    li.innerHTML = `<span>${sala}</span><span><strong>${copias} cópias</strong></span>`;
                    lista.appendChild(li);
                });
        }

        function atualizarFiltroSalas() {
            const salas = [...new Set(impressoes.map(imp => imp.sala))].sort();
            const select = document.getElementById('filtroSala');
            select.innerHTML = '<option value="">Todas as Turmas</option>';
            salas.forEach(sala => {
                select.innerHTML += `<option value="${sala}">${sala}</option>`;
            });
        }

        // Filtros
        window.filtrarTabela = function() {
            const operador = document.getElementById('filtroOperador').value;
            const impressora = document.getElementById('filtroImpressora').value;
            const tipo = document.getElementById('filtroTipo').value;
            const sala = document.getElementById('filtroSala').value;

            let filtrado = impressoes;

            if (operador) filtrado = filtrado.filter(imp => imp.operador === operador);
            if (impressora) filtrado = filtrado.filter(imp => imp.impressora === impressora);
            if (tipo) filtrado = filtrado.filter(imp => imp.tipo === tipo);
            if (sala) filtrado = filtrado.filter(imp => imp.sala === sala);

            atualizarTabela(filtrado);
        };

        window.filtrarPorData = function() {
            const inicio = document.getElementById('dataInicio').value;
            const fim = document.getElementById('dataFim').value;

            if (!inicio || !fim) {
                showNotification('Selecione as datas de início e fim', 'error');
                return;
            }

            const dataInicio = new Date(inicio);
            const dataFim = new Date(fim);
            dataFim.setHours(23, 59, 59);

            const filtrado = impressoes.filter(imp => {
                const dataImp = new Date(imp.dataObj);
                return dataImp >= dataInicio && dataImp <= dataFim;
            });

            atualizarTabela(filtrado);
            showNotification(`Exibindo ${filtrado.length} impressões no período selecionado`);
        };

        window.limparFiltro = function() {
            document.getElementById('filtroOperador').value = '';
            document.getElementById('filtroImpressora').value = '';
            document.getElementById('filtroTipo').value = '';
            document.getElementById('filtroSala').value = '';
            document.getElementById('dataInicio').value = '';
            document.getElementById('dataFim').value = '';
            atualizarTabela(impressoes);
        };

        // Ações
        window.excluirImpressao = async function(id) {
            if (confirm('Tem certeza que deseja excluir esta impressão?')) {
                try {
                    const imp = impressoes.find(i => i.id === id);
                    if (imp) {
                        const total = imp.folhas * imp.copias;
                        quotaUsada = Math.max(0, quotaUsada - total);
                        await salvarQuota();
                    }

                    await deleteDoc(doc(db, COLLECTION_NAME, id));
                    showNotification('Impressão excluída com sucesso!');
                } catch (error) {
                    console.error('Erro ao excluir:', error);
                    showNotification('Erro ao excluir impressão.', 'error');
                }
            }
        };

        window.editarImpressao = function(id) {
            const imp = impressoes.find(i => i.id === id);
            if (!imp) return;

            document.getElementById('editId').value = id;
            document.getElementById('editData').value = imp.dataImpressao || new Date(imp.dataObj).toISOString().split('T')[0];
            document.getElementById('editTipo').value = imp.tipo;
            document.getElementById('editSala').value = imp.sala;
            document.getElementById('editArquivo').value = imp.arquivo;
            document.getElementById('editFolhas').value = imp.folhas;
            document.getElementById('editCopias').value = imp.copias;

            document.getElementById('editModal').style.display = 'flex';
        };

        document.getElementById('editForm').addEventListener('submit', async function(e) {
            e.preventDefault();

            const id = document.getElementById('editId').value;
            const imp = impressoes.find(i => i.id === id);

            if (imp) {
                const totalAntigo = imp.folhas * imp.copias;

                const novosDados = {
                    dataImpressao: document.getElementById('editData').value,
                    data: new Date(document.getElementById('editData').value).toLocaleDateString('pt-BR'),
                    dataObj: new Date(document.getElementById('editData').value + 'T' + new Date().toTimeString().split(' ')[0]).toISOString(),
                    tipo: document.getElementById('editTipo').value,
                    sala: document.getElementById('editSala').value,
                    arquivo: document.getElementById('editArquivo').value,
                    folhas: parseInt(document.getElementById('editFolhas').value),
                    copias: parseInt(document.getElementById('editCopias').value)
                };

                try {
                    await updateDoc(doc(db, COLLECTION_NAME, id), novosDados);

                    const totalNovo = novosDados.folhas * novosDados.copias;
                    quotaUsada = quotaUsada - totalAntigo + totalNovo;
                    await salvarQuota();
                    atualizarQuota();

                    fecharModal();
                    showNotification('Impressão atualizada com sucesso!');
                } catch (error) {
                    console.error('Erro ao atualizar:', error);
                    showNotification('Erro ao atualizar impressão.', 'error');
                }
            }
        });

        window.fecharModal = function() {
            document.getElementById('editModal').style.display = 'none';
        };

        window.limparTudo = async function() {
            if (confirm('ATENÇÃO: Isso apagará TODOS os dados de impressões e resetará a cota. Deseja continuar?')) {
                try {
                    const snapshot = await getDocs(collection(db, COLLECTION_NAME));
                    const batch = [];
                    snapshot.forEach((doc) => {
                        batch.push(deleteDoc(doc.ref));
                    });
                    await Promise.all(batch);

                    quotaUsada = 0;
                    await salvarQuota();

                    showNotification('Todos os dados foram apagados');
                } catch (error) {
                    console.error('Erro ao limpar:', error);
                    showNotification('Erro ao limpar dados.', 'error');
                }
            }
        };

        // Exportação
        window.exportarCSV = function() {
            if (impressoes.length === 0) {
                showNotification('Não há dados para exportar', 'error');
                return;
            }

            let csv = 'Data,Tipo,Turma,Descrição,Impressora,Operador,Formato,Cor,Frente/Verso,Folhas,Cópias,Total,Observações\n';

            impressoes.forEach(imp => {
                const total = imp.folhas * imp.copias;
                csv += `"${imp.data}","${imp.tipo}","${imp.sala}","${imp.arquivo}","${imp.impressora}","${imp.operador}","${imp.formato}","${imp.tipoImpressao}","${imp.frenteVerso}",${imp.folhas},${imp.copias},${total},"${imp.observacoes || ''}"\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `impressoes_${new Date().toISOString().split('T')[0]}.csv`;
            link.click();

            showNotification('Arquivo CSV exportado com sucesso!');
        };

        window.exportarPDF = function() {
            showNotification('Para PDF, use a função de imprimir (Ctrl+P) e salve como PDF', 'error');
        };

        // Utilitários
        function getMesAno() {
            const data = new Date();
            return data.getFullYear() + '-' + String(data.getMonth() + 1).padStart(2, '0');
        }

        function showNotification(msg, type = 'success') {
            notification.textContent = msg;
            notification.className = 'notification ' + (type === 'error' ? 'error' : '');
            notification.classList.add('show');

            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Fechar modal ao clicar fora
        window.onclick = function(event) {
            const modal = document.getElementById('editModal');
            if (event.target === modal) {
                fecharModal();
            }
        };
    </script>
</body>
</html>
