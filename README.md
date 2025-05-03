# 📦 Classe Backup ADVPL para TOTVS Protheus

[![ADVPL](https://img.shields.io/badge/Language-ADVPL-blue)](https://www.totvs.com.br)
[![Protheus](https://img.shields.io/badge/ERP-Protheus-success)](https://www.totvs.com.br/protheus/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

Solução para backup de tabelas no Protheus, gerando arquivos `.DTC` para possibilitar o append pela apsdu, caso necessário.

## Índice
- [Funcionalidades](#-funcionalidades)
- [Como Usar](#-como-usar)
- [Estrutura de Arquivos](#-estrutura-de-arquivos)
- [Pré-requisitos](#-pré-requisitos)
- [Roadmap](#-roadmap)
- [Contribuição](#-contribuição)
- [Licença](#-licença)

## 🔧 Funcionalidades

| Feature | Descrição |
|---------|-----------|
| **Backup Completo** | Estrutura + dados + índices em `.DTC` |
| **Filtros Dinâmicos** | Sintaxe ADVPL nativa (ex: `"SA1->A1_STATUS == 'A'"`) |
| **Organização Automática** | Pastas por tabela/data/hora |
| **Tratamento de Erros** | Notificação visual sem quebrar execução |
| **Verificação** | Propriedade `_lBackUpRealizado` para checagem |

## 🚀 Como Usar

```advpl
// 1. Backup completo
oBackup := Backup():New("SB1")

// 2. Backup com filtro
oBackupFiltrado := Backup():New("SA1", "A1_FILIAL == '01' .AND. A1_MSBLQL != '1'")

// 3. Verificação
If oBackup:_lBackUpRealizado
   FwAlertInfo("Backup realizado com sucesso!", "Operação concluída")
Else
   FwAlertError("Falha no backup", "Atenção")
EndIf
```

## 📁 Estrutura de Arquivos
```
system/
└── backup/
    └── [TABELA]_[AAAAMMDD]/
        └── [HH-MM-SS]/
            ├── [TABELA]_[DATA]_[HORA].dtc
```
Exemplo real:
```
C:\TOTVS\Protheus12\system\backup\SA1_20240520\14-30-00\
├── SA1_20240520_14-30-00.dtc
└── ctreeint/
    ├── SA1_20240520_14-30-00dtc.lck
    ├── SA1_20240520_14-30-00dtc.int
```

## 📌 Pré-requisitos
- [TLPP Include](https://tdn.totvs.com/pages/viewpage.action?pageId=619741238) (include obrigatório)
- Permissões de escrita no servidor
- Espaço disponível no servidor

## 🛠️ Roadmap
✔️ **Versão 1.0** - Backup básico  
🔜 **Versão 1.1** - Validação de campos nos filtros  
🔜 **Versão 1.2** - Progresso visual (barra de carregamento)  
🔜 **Versão 2.0** - Envio automático por e-mail  
🔜 **Versão 3.0** - Estudar possibilidade de validar o S.O do servidor de aplicação.  

## 🤝 Contribuição
1. Faça um fork do projeto
2. Crie sua branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'Add some feature'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## 📄 Licença
Distribuído sob licença MIT. Veja [LICENSE](LICENSE) para detalhes.

---
**Desenvolvido por** [Mateus Pragana](https://github.com/seu-usuario)  
**Última atualização**: 02/05/2025
