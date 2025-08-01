<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bbce3572338711aeab758506379ab716",
  "translation_date": "2025-07-12T13:43:49+00:00",
  "source_file": "11-mcp/README.md",
  "language_code": "fr"
}
-->
# Leçon 11 : Intégration du Model Context Protocol (MCP)

## Introduction au Model Context Protocol (MCP)

Le Model Context Protocol (MCP) est un cadre innovant conçu pour standardiser les interactions entre les modèles d’IA et les applications clientes. MCP fait office de passerelle entre les modèles d’IA et les applications qui les utilisent, offrant une interface cohérente quel que soit le modèle sous-jacent.

Points clés du MCP :

- **Communication standardisée** : MCP établit un langage commun pour que les applications communiquent avec les modèles d’IA
- **Gestion améliorée du contexte** : Permet de transmettre efficacement des informations contextuelles aux modèles d’IA
- **Compatibilité multiplateforme** : Fonctionne avec plusieurs langages de programmation dont C#, Java, JavaScript, Python et TypeScript
- **Intégration fluide** : Facilite l’intégration de différents modèles d’IA dans les applications

Le MCP est particulièrement utile dans le développement d’agents IA car il permet aux agents d’interagir avec divers systèmes et sources de données via un protocole unifié, rendant les agents plus flexibles et puissants.

## Objectifs d’apprentissage
- Comprendre ce qu’est le MCP et son rôle dans le développement d’agents IA
- Installer et configurer un serveur MCP pour l’intégration GitHub
- Construire un système multi-agent avec les outils MCP
- Implémenter le RAG (Retrieval Augmented Generation) avec Azure Cognitive Search

## Prérequis
- Python 3.8+
- Node.js 14+
- Abonnement Azure
- Compte GitHub
- Connaissances de base sur Semantic Kernel

## Instructions d’installation

1. **Configuration de l’environnement**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Configurer les services Azure**
   - Créer une ressource Azure Cognitive Search
   - Configurer le service Azure OpenAI
   - Définir les variables d’environnement dans `.env`

3. **Installation du serveur MCP**
   ```bash
   npm install -g @modelcontextprotocol/server-github
   ```

## Structure du projet

```
11-mcp/
├── code_samples/
│   └── github-mcp/
│       ├── app.py              # Main application
│       ├── event-descriptions.md  # Event data
│       └── MCP_SETUP.md        # Setup guide
├── README.md
└── requirements.txt
```

## Composants principaux

### 1. Système multi-agent
- Agent GitHub : Analyse de dépôts
- Agent Hackathon : Recommandations de projets
- Agent Événements : Suggestions d’événements tech

### 2. Intégration Azure
- Cognitive Search pour l’indexation des événements
- Azure OpenAI pour l’intelligence des agents
- Implémentation du pattern RAG

### 3. Outils MCP
- Analyse de dépôts GitHub
- Inspection de code
- Extraction de métadonnées

## Parcours du code

L’exemple montre :
1. Intégration du serveur MCP
2. Orchestration multi-agent
3. Intégration d’Azure Cognitive Search
4. Implémentation du pattern RAG

Fonctionnalités clés :
- Analyse en temps réel des dépôts GitHub
- Recommandations intelligentes de projets
- Correspondance d’événements via Azure Search
- Réponses en streaming avec Chainlit

## Exécution de l’exemple

Pour des instructions détaillées et plus d’informations, consultez le [Github MCP Server Example README](./code_samples/github-mcp/README.md).

1. Démarrer le serveur MCP :
   ```bash
   npx @modelcontextprotocol/server-github
   ```

2. Lancer l’application :
   ```bash
   chainlit run app.py -w
   ```

3. Tester l’intégration :
   ```
   Example query: "Analyze repositories for username: <github_username>"
   ```

## Dépannage

Problèmes courants et solutions :
1. Problèmes de connexion MCP
   - Vérifier que le serveur est en fonctionnement
   - Contrôler la disponibilité du port
   - Confirmer les tokens GitHub

2. Problèmes Azure Search
   - Valider les chaînes de connexion
   - Vérifier l’existence de l’index
   - Confirmer le téléchargement des documents

## Étapes suivantes
- Explorer d’autres outils MCP
- Implémenter des agents personnalisés
- Améliorer les capacités RAG
- Ajouter plus de sources d’événements

## Ressources
- [MCP for Beginners](https://aka.ms/mcp-for-beginners)  
- [MCP Documentation](https://github.com/microsoft/semantic-kernel/tree/main/python/semantic-kernel/semantic_kernel/connectors/mcp)
- [Azure Cognitive Search Docs](https://learn.microsoft.com/azure/search/)
- [Semantic Kernel Guides](https://learn.microsoft.com/semantic-kernel/)

**Avertissement** :  
Ce document a été traduit à l’aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d’assurer l’exactitude, veuillez noter que les traductions automatiques peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d’origine doit être considéré comme la source faisant foi. Pour les informations critiques, une traduction professionnelle réalisée par un humain est recommandée. Nous déclinons toute responsabilité en cas de malentendus ou de mauvaises interprétations résultant de l’utilisation de cette traduction.