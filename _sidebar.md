<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guia de Proteção de Dados - Setor Público</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            display: flex;
            min-height: 100vh;
            background-color: #f0f2f5;
        }

        /* Sidebar */
        .sidebar {
            width: 380px;
            background: linear-gradient(180deg, #1a3b5d 0%, #0f2a44 100%);
            color: white;
            height: 100vh;
            overflow-y: auto;
            box-shadow: 4px 0 15px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }

        .sidebar-header {
            padding: 25px 20px;
            background: rgba(255,255,255,0.1);
            border-bottom: 2px solid #2a4f73;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .sidebar-header h2 {
            font-size: 1.5rem;
            font-weight: 300;
            letter-spacing: 1px;
        }

        .sidebar-header h2 span {
            font-weight: 700;
            color: #ffd966;
        }

        .sidebar-header p {
            font-size: 0.85rem;
            opacity: 0.8;
            margin-top: 5px;
        }

        .home-button {
            background-color: #ffd966;
            color: #1a3b5d;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
            transition: all 0.2s;
            border: 1px solid transparent;
        }

        .home-button:hover {
            background-color: #ffe599;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .menu-container {
            padding: 15px;
        }

        /* Módulos */
        .modulo {
            margin-bottom: 12px;
            border-radius: 10px;
            overflow: hidden;
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1);
            transition: all 0.3s;
        }

        .modulo:hover {
            background: rgba(255,255,255,0.1);
            border-color: rgba(255,255,255,0.2);
        }

        .modulo-header {
            padding: 15px 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-weight: 600;
            font-size: 1.1rem;
            user-select: none;
        }

        .modulo-header .emoji {
            font-size: 1.3rem;
            margin-right: 10px;
        }

        .modulo-header .arrow {
            font-size: 1.2rem;
            transition: transform 0.3s;
        }

        .modulo.active .modulo-header {
            background: rgba(255,215,0,0.15);
            border-bottom: 1px solid #ffd966;
        }

        .modulo.active .arrow {
            transform: rotate(90deg);
        }

        .modulo-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out;
            background: rgba(0,0,0,0.2);
        }

        .modulo.active .modulo-content {
            max-height: 800px; /* Ajuste conforme necessário */
            transition: max-height 0.7s ease-in;
        }

        /* Itens do módulo */
        .modulo-item {
            padding: 12px 20px 12px 50px;
            cursor: pointer;
            font-size: 0.95rem;
            border-bottom: 1px solid rgba(255,255,255,0.05);
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.2s;
            color: rgba(255,255,255,0.9);
        }

        .modulo-item:hover {
            background: rgba(255,215,0,0.2);
            padding-left: 60px;
            color: white;
        }

        .modulo-item .item-emoji {
            font-size: 1rem;
            opacity: 0.7;
        }

        .modulo-item.active-item {
            background: rgba(255,215,0,0.3);
            border-left: 4px solid #ffd966;
            color: white;
            font-weight: 500;
        }

        /* Área de conteúdo principal */
        .main-content {
            flex: 1;
            padding: 30px 40px;
            overflow-y: auto;
            background-color: #f8f9fa;
        }

        .content-card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.05);
            min-height: 100%;
            border: 1px solid #e9ecef;
        }

        .content-card h1 {
            color: #1a3b5d;
            font-size: 2rem;
            margin-bottom: 20px;
            border-bottom: 3px solid #ffd966;
            padding-bottom: 10px;
        }

        .content-card h2 {
            color: #2c3e50;
            margin: 25px 0 15px;
            font-size: 1.5rem;
        }

        .content-card h3 {
            color: #34495e;
            margin: 20px 0 10px;
            font-size: 1.2rem;
        }

        .content-card p {
            line-height: 1.6;
            color: #444;
            margin-bottom: 15px;
        }

        .content-card ul, .content-card ol {
            margin: 10px 0 20px 25px;
            color: #555;
        }

        .content-card li {
            margin-bottom: 8px;
        }

        .back-to-menu {
            display: inline-block;
            background: #e9ecef;
            color: #1a3b5d;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            margin-bottom: 20px;
            font-weight: 600;
            transition: all 0.2s;
            border: 1px solid #dee2e6;
        }

        .back-to-menu:hover {
            background: #dee2e6;
            transform: translateX(-5px);
        }

        .home-indicator {
            background: #ffd966;
            color: #1a3b5d;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 600;
            display: inline-block;
            margin-bottom: 15px;
        }

        /* Scrollbar personalizada */
        .sidebar::-webkit-scrollbar {
            width: 6px;
        }

        .sidebar::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.1);
        }

        .sidebar::-webkit-scrollbar-thumb {
            background: #ffd966;
            border-radius: 3px;
        }

        /* Responsividade */
        @media (max-width: 768px) {
            body {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: 300px;
            }
            
            .main-content {
                padding: 20px;
            }
        }

        /* Dicas visuais */
        .tip {
            background: #e1f5fe;
            border-left: 4px solid #0288d1;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
        }

        .warning {
            background: #fff3e0;
            border-left: 4px solid #ff9800;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <!-- Sidebar -->
    <div class="sidebar">
        <div class="sidebar-header">
            <h2>🔐 <span>Proteção de Dados</span></h2>
            <p>Guia completo para o Setor Público</p>
            <button class="home-button" onclick="showHome()">🏠 Menu Principal</button>
        </div>
        
        <div class="menu-container" id="menuContainer">
            <!-- Módulo 1 -->
            <div class="modulo" id="modulo1">
                <div class="modulo-header" onclick="toggleModulo('modulo1')">
                    <span><span class="emoji">🔒</span> MÓDULO 1: SEGURANÇA DA INFORMAÇÃO</span>
                    <span class="arrow">▶</span>
                </div>
                <div class="modulo-content">
                    <div class="modulo-item" onclick="loadContent('fundamentos')">
                        <span class="item-emoji">🔐</span> Fundamentos de Segurança
                    </div>
                    <div class="modulo-item" onclick="loadContent('ameacas')">
                        <span class="item-emoji">⚠️</span> Principais ameaças
                    </div>
                    <div class="modulo-item" onclick="loadContent('boasPraticas')">
                        <span class="item-emoji">👤</span> Boas práticas para servidores
                    </div>
                    <div class="modulo-item" onclick="loadContent('incidentes')">
                        <span class="item-emoji">🚨</span> Gestão de incidentes
                    </div>
                    <div class="modulo-item" onclick="loadContent('governanca')">
                        <span class="item-emoji">🏛️</span> Governança de segurança
                    </div>
                </div>
            </div>

            <!-- Módulo 2 -->
            <div class="modulo" id="modulo2">
                <div class="modulo-header" onclick="toggleModulo('modulo2')">
                    <span><span class="emoji">📘</span> MÓDULO 2: LGPD</span>
                    <span class="arrow">▶</span>
                </div>
                <div class="modulo-content">
                    <div class="modulo-item" onclick="loadContent('lgpdIntroducao')">
                        <span class="item-emoji">📘</span> Introdução à LGPD
                    </div>
                    <div class="modulo-item" onclick="loadContent('dadosPessoais')">
                        <span class="item-emoji">👥</span> Dados pessoais
                    </div>
                    <div class="modulo-item" onclick="loadContent('dadosAnonimizados')">
                        <span class="item-emoji">🔢</span> Dados anonimizados
                    </div>
                    <div class="modulo-item" onclick="loadContent('dadosPublicos')">
                        <span class="item-emoji">🌐</span> Dados públicos
                    </div>
                    <div class="modulo-item" onclick="loadContent('agentes')">
                        <span class="item-emoji">⚙️</span> Agentes de tratamento
                    </div>
                    <div class="modulo-item" onclick="loadContent('principios')">
                        <span class="item-emoji">📋</span> 10 princípios da LGPD
                    </div>
                    <div class="modulo-item" onclick="loadContent('direitos')">
                        <span class="item-emoji">🔑</span> Direitos dos titulares
                    </div>
                    <div class="modulo-item" onclick="loadContent('fiscalizacao')">
                        <span class="item-emoji">⚖️</span> Fiscalização e penalidades
                    </div>
                    <div class="modulo-item" onclick="loadContent('governancaLgpd')">
                        <span class="item-emoji">🛡️</span> Segurança e boas práticas
                    </div>
                    <div class="modulo-item" onclick="loadContent('gdpr')">
                        <span class="item-emoji">🇪🇺</span> LGPD x GDPR
                    </div>
                </div>
            </div>

            <!-- Módulo 3 -->
            <div class="modulo" id="modulo3">
                <div class="modulo-header" onclick="toggleModulo('modulo3')">
                    <span><span class="emoji">📢</span> MÓDULO 3: LAI</span>
                    <span class="arrow">▶</span>
                </div>
                <div class="modulo-content">
                    <div class="modulo-item" onclick="loadContent('laiIntroducao')">
                        <span class="item-emoji">📢</span> Introdução à LAI
                    </div>
                    <div class="modulo-item" onclick="loadContent('direitosCidadao')">
                        <span class="item-emoji">👥</span> Direitos do cidadão
                    </div>
                    <div class="modulo-item" onclick="loadContent('obrigacoesPublico')">
                        <span class="item-emoji">🏢</span> Obrigações do poder público
                    </div>
                    <div class="modulo-item" onclick="loadContent('limitesExcecoes')">
                        <span class="item-emoji">🔒</span> Limites e exceções
                    </div>
                    <div class="modulo-item" onclick="loadContent('conciliacaoLgpdLai')">
                        <span class="item-emoji">🤝</span> LGPD x LAI: como conciliar?
                    </div>
                    <div class="modulo-item" onclick="loadContent('recursos')">
                        <span class="item-emoji">🔄</span> Recursos e instâncias
                    </div>
                </div>
            </div>

            <!-- Módulo 4 -->
            <div class="modulo" id="modulo4">
                <div class="modulo-header" onclick="toggleModulo('modulo4')">
                    <span><span class="emoji">💡</span> MÓDULO 4: INOVAÇÃO</span>
                    <span class="arrow">▶</span>
                </div>
                <div class="modulo-content">
                    <div class="modulo-item" onclick="loadContent('transformacaoDigital')">
                        <span class="item-emoji">💡</span> Transformação Digital
                    </div>
                    <div class="modulo-item" onclick="loadContent('tecnologiasEmergentes')">
                        <span class="item-emoji">🤖</span> Tecnologias emergentes
                    </div>
                    <div class="modulo-item" onclick="loadContent('privacidadeInovacao')">
                        <span class="item-emoji">🔐</span> Privacidade e inovação
                    </div>
                    <div class="modulo-item" onclick="loadContent('eticaInovacao')">
                        <span class="item-emoji">⚖️</span> Ética e proteção de dados
                    </div>
                    <div class="modulo-item" onclick="loadContent('casosSucesso')">
                        <span class="item-emoji">🏆</span> Casos de sucesso
                    </div>
                    <div class="modulo-item" onclick="loadContent('futuro')">
                        <span class="item-emoji">🚀</span> Futuro da proteção de dados
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Área de conteúdo principal -->
    <div class="main-content" id="mainContent">
        <div class="content-card" id="contentCard">
            <!-- Conteúdo será carregado dinamicamente aqui -->
            <div class="home-indicator">🏠 Você está na página inicial</div>
            <h1>📚 Guia de Proteção de Dados para o Setor Público</h1>
            
            <p>Bem-vindo ao guia completo sobre <strong>Segurança da Informação, LGPD, LAI e Inovação</strong> no serviço público. Este material foi desenvolvido para auxiliar servidores públicos a compreender e aplicar as melhores práticas de proteção de dados em seu dia a dia.</p>

            <h2>🎯 Objetivos do Guia</h2>
            <ul>
                <li>Compreender os fundamentos de Segurança da Informação</li>
                <li>Dominar os conceitos e aplicações da LGPD no setor público</li>
                <li>Conciliar a proteção de dados com a transparência exigida pela LAI</li>
                <li>Explorar tendências de inovação com responsabilidade</li>
            </ul>

            <h2>📌 Como navegar</h2>
            <p>Clique nos módulos na barra lateral para expandir e acessar os conteúdos específicos. Cada tópico abrirá seu conteúdo detalhado nesta área principal. Use o botão "Menu Principal" a qualquer momento para retornar a esta página inicial.</p>

            <div class="tip">
                <strong>💡 Dica:</strong> Os módulos foram organizados de forma progressiva. Recomendamos começar pelo Módulo 1 para construir uma base sólida antes de avançar.
            </div>

            <h2>📋 Visão geral dos módulos</h2>
            <ul>
                <li><strong>Módulo 1 - Segurança da Informação:</strong> Fundamentos, ameaças, boas práticas e governança</li>
                <li><strong>Módulo 2 - LGPD:</strong> Lei Geral de Proteção de Dados aplicada ao serviço público</li>
                <li><strong>Módulo 3 - LAI:</strong> Lei de Acesso à Informação e sua relação com a proteção de dados</li>
                <li><strong>Módulo 4 - Inovação:</strong> Novas tecnologias e o futuro da proteção de dados</li>
            </ul>

            <div class="warning">
                <strong>⚠️ Importante:</strong> Este guia é um material de apoio e não substitui a consulta à legislação vigente e orientações oficiais dos órgãos competentes.
            </div>
        </div>
    </div>

    <script>
        // Função para alternar a abertura/fechamento dos módulos
        function toggleModulo(moduloId) {
            const modulo = document.getElementById(moduloId);
            modulo.classList.toggle('active');
            
            // Fecha os outros módulos (opcional - para manter apenas um aberto)
            const modulos = document.querySelectorAll('.modulo');
            modulos.forEach(m => {
                if (m.id !== moduloId && m.classList.contains('active')) {
                    m.classList.remove('active');
                }
            });
        }

        // Função para carregar conteúdo dinâmico
        function loadContent(contentId) {
            const mainContent = document.getElementById('contentCard');
            
            // Remove a classe active-item de todos os itens
            document.querySelectorAll('.modulo-item').forEach(item => {
                item.classList.remove('active-item');
            });
            
            // Adiciona classe active-item ao item clicado
            event.currentTarget.classList.add('active-item');
            
            // Mapeamento de conteúdos (simulado - aqui você adicionaria o conteúdo real)
            const contents = {
                // Módulo 1
                fundamentos: {
                    title: '🔒 Fundamentos de Segurança da Informação',
                    content: `
                        <div class="home-indicator">📖 Módulo 1: Segurança da Informação</div>
                        <h1>Fundamentos de Segurança da Informação</h1>
                        
                        <h2>O que é Segurança da Informação?</h2>
                        <p>A segurança da informação é a prática de proteger informações contra acesso, uso, divulgação, interrupção, modificação ou destruição não autorizados. No setor público, isso é ainda mais crítico devido ao volume de dados pessoais e sensíveis dos cidadãos.</p>
                        
                        <h2>Pilares da segurança (CID)</h2>
                        <ul>
                            <li><strong>Confidencialidade:</strong> Garantir que a informação seja acessível apenas por pessoas autorizadas.</li>
                            <li><strong>Integridade:</strong> Assegurar que a informação não seja alterada de forma não autorizada.</li>
                            <li><strong>Disponibilidade:</strong> Garantir que a informação esteja disponível quando necessário.</li>
                        </ul>
                        
                        <h2>Segurança da Informação vs Cibersegurança</h2>
                        <p>Enquanto a segurança da informação abrange todos os aspectos de proteção de dados (físicos, digitais, humanos), a cibersegurança foca especificamente na proteção de sistemas e redes contra ataques digitais.</p>
                        
                        <div class="tip">
                            <strong>Para o servidor público:</strong> A segurança começa com pequenas ações diárias, como não compartilhar senhas, manter softwares atualizados e desconfiar de e-mails suspeitos.
                        </div>
                    `
                },
                ameacas: {
                    title: '⚠️ Principais ameaças e vulnerabilidades',
                    content: `
                        <div class="home-indicator">📖 Módulo 1: Segurança da Informação</div>
                        <h1>Principais ameaças e vulnerabilidades</h1>
                        
                        <h2>Phishing, engenharia social e ransomware</h2>
                        <p><strong>Phishing:</strong> Técnica de engenharia social que usa comunicações falsas (e-mails, SMS) para enganar usuários e obter informações sensíveis.</p>
                        <p><strong>Ransomware:</strong> Malware que sequestra dados e exige resgate. Órgãos públicos são alvos frequentes.</p>
                        
                        <h2>Ameaças internas vs externas</h2>
                        <ul>
                            <li><strong>Internas:</strong> Funcionários mal-intencionados ou descuidados</li>
                            <li><strong>Externas:</strong> Hackers, criminosos cibernéticos, estados-nação</li>
                        </ul>
                        
                        <h2>Vulnerabilidades comuns em sistemas públicos</h2>
                        <ul>
                            <li>Sistemas legados desatualizados</li>
                            <li>Falta de treinamento de servidores</li>
                            <li>Configurações incorretas de segurança</li>
                            <li>Senhas fracas ou reutilizadas</li>
                        </ul>
                        
                        <div class="warning">
                            <strong>Alerta:</strong> O setor público brasileiro sofreu um aumento de 300% nos ataques de ransomware nos últimos anos.
                        </div>
                    `
                },
                boasPraticas: {
                    title: '👤 Boas práticas para o servidor público',
                    content: `
                        <div class="home-indicator">📖 Módulo 1: Segurança da Informação</div>
                        <h1>Boas práticas para o servidor público</h1>
                        
                        <h2>Uso seguro de senhas e autenticação multifator</h2>
                        <ul>
                            <li>Use senhas longas (mínimo 12 caracteres) com combinação de letras, números e símbolos</li>
                            <li>Ative a autenticação de dois fatores (2FA) sempre que possível</li>
                            <li>Nunca reutilize senhas entre sistemas pessoais e corporativos</li>
                            <li>Use gerenciadores de senhas</li>
                        </ul>
                        
                        <h2>Cuidados com e-mails e links suspeitos</h2>
                        <ul>
                            <li>Verifique o remetente antes de abrir anexos</li>
                            <li>Passe o mouse sobre links para ver o destino real</li>
                            <li>Desconfie de mensagens com senso de urgência</li>
                            <li>Não forneça credenciais por e-mail ou telefone</li>
                        </ul>
                        
                        <h2>Segurança no trabalho remoto</h2>
                        <ul>
                            <li>Use VPN para acessar sistemas internos</li>
                            <li>Mantenha o software do dispositivo atualizado</li>
                            <li>Proteja a tela de visões não autorizadas</li>
                            <li>Não use redes Wi-Fi públicas sem proteção</li>
                            <li>Bloqueie a tela ao se ausentar</li>
                        </ul>
                        
                        <div class="tip">
                            <strong>Lembre-se:</strong> Você é a primeira linha de defesa contra ataques cibernéticos!
                        </div>
                    `
                },
                incidentes: {
                    title: '🚨 Gestão de incidentes de segurança',
                    content: `
                        <div class="home-indicator">📖 Módulo 1: Segurança da Informação</div>
                        <h1>Gestão de incidentes de segurança</h1>
                        
                        <h2>O que fazer em caso de vazamento de dados?</h2>
                        <ol>
                            <li><strong>Isolar:</strong> Desconecte o dispositivo afetado da rede</li>
                            <li><strong>Comunicar:</strong> Avise imediatamente a equipe de TI e o DPO</li>
                            <li><strong>Documentar:</strong> Registre todos os detalhes do incidente</li>
                            <li><strong>Não alterar:</strong> Não tente "consertar" sozinho - preserve as evidências</li>
                        </ol>
                        
                        <h2>Plano de resposta a incidentes</h2>
                        <ul>
                            <li>Preparação: treinamentos e ferramentas</li>
                            <li>Identificação: detecção do incidente</li>
                            <li>Contenção: limitar os danos</li>
                            <li>Erradicação: remover a causa</li>
                            <li>Recuperação: restaurar sistemas</li>
                            <li>Lições aprendidas: melhorias contínuas</li>
                        </ul>
                        
                        <h2>Obrigações legais de notificação (LGPD)</h2>
                        <p>A LGPD exige a comunicação à ANPD e aos titulares em caso de incidentes que possam acarretar risco ou dano relevante. O prazo é de <strong>5 dias úteis</strong> após a ciência.</p>
                        
                        <div class="warning">
                            <strong>Multa:</strong> A não notificação pode resultar em multas de até 2% do faturamento (limitada a R$ 50 milhões por infração).
                        </div>
                    `
                },
                governanca: {
                    title: '🏛️ Governança de segurança no setor público',
                    content: `
                        <div class="home-indicator">📖 Módulo 1: Segurança da Informação</div>
                        <h1>Governança de segurança no setor público</h1>
                        
                        <h2>Políticas de segurança da informação (POSIT)</h2>
                        <p>A Política de Segurança da Informação (POSIT) é o documento que estabelece as diretrizes, responsabilidades e regras para proteger os ativos de informação do órgão.</p>
                        
                        <h2>Comitês de segurança e privacidade</h2>
                        <p>Estrutura multidisciplinar responsável por:</p>
                        <ul>
                            <li>Aprovar políticas e normas</li>
                            <li>Analisar incidentes críticos</li>
                            <li>Orientar investimentos em segurança</li>
                            <li>Promover a cultura de privacidade</li>
                        </ul>
                        
                        <h2>Normas complementares e instruções normativas</h2>
                        <ul>
                            <li><strong>IN GSI/PR nº 1/2020:</strong> Estrutura de segurança cibernética</li>
                            <li><strong>IN SGD/ME nº 94/2022:</strong> Segurança em contratações de TI</li>
                            <li><strong>Decreto nº 10.222/2020:</strong> Estratégia Nacional de Segurança Cibernética</li>
                        </ul>
                    `
                },
                
                // Módulo 2 - LGPD (apenas alguns exemplos para não ficar muito longo)
                lgpdIntroducao: {
                    title: '📘 Introdução à LGPD',
                    content: `
                        <div class="home-indicator">📖 Módulo 2: LGPD</div>
                        <h1>Introdução à LGPD</h1>
                        
                        <h2>O que é LGPD?</h2>
                        <p>A Lei Geral de Proteção de Dados (Lei nº 13.709/2018) regula as atividades de tratamento de dados pessoais, inclusive nos meios digitais, com o objetivo de proteger os direitos fundamentais de liberdade e de privacidade.</p>
                        
                        <h2>Importância para o serviço público</h2>
                        <p>Órgãos públicos são os maiores detentores de dados dos cidadãos. A LGPD impõe responsabilidades e estabelece limites para o uso dessas informações, garantindo maior transparência e controle social.</p>
                        
                        <h2>O que é ANPD?</h2>
                        <p>A Autoridade Nacional de Proteção de Dados (ANPD) é o órgão responsável por fiscalizar, regulamentar e orientar a aplicação da LGPD no Brasil.</p>
                        
                        <h2>O que a lei considera como tratamento de dados?</h2>
                        <p>Toda operação realizada com dados pessoais: coleta, produção, recepção, classificação, utilização, acesso, reprodução, transmissão, distribuição, processamento, arquivamento, armazenamento, eliminação, avaliação ou controle da informação, modificação, comunicação, transferência, difusão ou extração.</p>
                    `
                },
                dadosPessoais: {
                    title: '👥 Dados pessoais',
                    content: `
                        <div class="home-indicator">📖 Módulo 2: LGPD</div>
                        <h1>Dados pessoais</h1>
                        
                        <h2>O que são dados pessoais?</h2>
                        <p>Informação relacionada a pessoa natural identificada ou identificável. Exemplos: nome, CPF, RG, endereço, telefone, dados de localização, IP, etc.</p>
                        
                        <h2>Todos os dados são considerados pessoais?</h2>
                        <p>Não. Dados anonimizados (que não permitem identificar o titular) não são considerados dados pessoais para fins da LGPD.</p>
                        
                        <h2>Como funciona o tratamento no setor público?</h2>
                        <p>O tratamento no setor público deve observar finalidades específicas e legais, como a execução de políticas públicas. O consentimento nem sempre é a base legal adequada - geralmente usa-se o cumprimento de obrigação legal ou a execução de políticas públicas.</p>
                        
                        <h2>O que são dados pessoais sensíveis?</h2>
                        <p>Dados sobre origem racial ou étnica, convicção religiosa, opinião política, filiação a sindicato, dados de saúde, vida sexual, dados genéticos ou biométricos. Têm proteção ainda mais rigorosa.</p>
                        
                        <div class="tip">
                            <strong>Atenção:</strong> Dados sensíveis só podem ser tratados em situações muito específicas previstas em lei.
                        </div>
                    `
                },
                
                // Adicione aqui os demais conteúdos seguindo o mesmo padrão...
            };
            
            // Carrega o conteúdo correspondente ou mostra mensagem de erro
            if (contents[contentId]) {
                mainContent.innerHTML = contents[contentId].content;
            } else {
                mainContent.innerHTML = `
                    <div class="home-indicator">📄 Conteúdo em desenvolvimento</div>
                    <h1>Conteúdo não encontrado</h1>
                    <p>O conteúdo solicitado ainda não foi adicionado ao sistema ou está em fase de elaboração.</p>
                    <button class="back-to-menu" onclick="showHome()">← Voltar ao menu principal</button>
                `;
            }
            
            // Rolagem suave para o topo
            document.querySelector('.main-content').scrollTop = 0;
        }

        // Função para mostrar a página inicial
        function showHome() {
            const mainContent = document.getElementById('contentCard');
            
            // Remove classe active-item de todos os itens
            document.querySelectorAll('.modulo-item').forEach(item => {
                item.classList.remove('active-item');
            });
            
            mainContent.innerHTML = `
                <div class="home-indicator">🏠 Você está na página inicial</div>
                <h1>📚 Guia de Proteção de Dados para o Setor Público</h1>
                
                <p>Bem-vindo ao guia completo sobre <strong>Segurança da Informação, LGPD, LAI e Inovação</strong> no serviço público. Este material foi desenvolvido para auxiliar servidores públicos a compreender e aplicar as melhores práticas de proteção de dados em seu dia a dia.</p>

                <h2>🎯 Objetivos do Guia</h2>
                <ul>
                    <li>Compreender os fundamentos de Segurança da Informação</li>
                    <li>Dominar os conceitos e aplicações da LGPD no setor público</li>
                    <li>Conciliar a proteção de dados com a transparência exigida pela LAI</li>
                    <li>Explorar tendências de inovação com responsabilidade</li>
                </ul>

                <h2>📌 Como navegar</h2>
                <p>Clique nos módulos na barra lateral para expandir e acessar os conteúdos específicos. Cada tópico abrirá seu conteúdo detalhado nesta área principal. Use o botão "Menu Principal" a qualquer momento para retornar a esta página inicial.</p>

                <div class="tip">
                    <strong>💡 Dica:</strong> Os módulos foram organizados de forma progressiva. Recomendamos começar pelo Módulo 1 para construir uma base sólida antes de avançar.
                </div>

                <h2>📋 Visão geral dos módulos</h2>
                <ul>
                    <li><strong>Módulo 1 - Segurança da Informação:</strong> Fundamentos, ameaças, boas práticas e governança</li>
                    <li><strong>Módulo 2 - LGPD:</strong> Lei Geral de Proteção de Dados aplicada ao serviço público</li>
                    <li><strong>Módulo 3 - LAI:</strong> Lei de Acesso à Informação e sua relação com a proteção de dados</li>
                    <li><strong>Módulo 4 - Inovação:</strong> Novas tecnologias e o futuro da proteção de dados</li>
                </ul>

                <div class="warning">
                    <strong>⚠️ Importante:</strong> Este guia é um material de apoio e não substitui a consulta à legislação vigente e orientações oficiais dos órgãos competentes.
                </div>
            `;
            
            // Rolagem suave para o topo
            document.querySelector('.main-content').scrollTop = 0;
        }

        // Opcional: Abrir módulo se um item for clicado (para melhor UX)
        document.querySelectorAll('.modulo-item').forEach(item => {
            item.addEventListener('click', function(e) {
                // Encontra o módulo pai e abre ele
                const modulo = this.closest('.modulo');
                if (modulo && !modulo.classList.contains('active')) {
                    modulo.classList.add('active');
                }
            });
        });
    </script>
</body>
</html>
