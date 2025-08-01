{
  "title": "Fantasy Creative Writing Project",
  "description": "Metadata schema for organizing a fantasy story’s drafts, world-building, characters, and chapters.",
  "type": "object",
  "properties": {
    "projectId": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for this project."
    },
    "title": {
      "type": "string",
      "minLength": 1,
      "description": "Project or story title."
    },
    "author": {
      "type": "string",
      "minLength": 1,
      "description": "Name of the writer."
    },
    "createdAt": {
      "type": "string",
      "format": "date-time",
      "description": "When the project was initialized."
    },
    "updatedAt": {
      "type": "string",
      "format": "date-time",
      "description": "Most recent update timestamp."
    },
    "status": {
      "type": "string",
      "enum": ["planning", "drafting", "revising", "complete"],
      "description": "Current phase of development."
    },
    "genre": {
      "type": "string",
      "enum": ["fantasy"],
      "description": "Genre of the project."
    },
    "tags": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Custom labels for filtering."
    },
    "setting": {
      "type": "object",
      "description": "Primary world and locale details.",
      "properties": {
        "worldName": { "type": "string" },
        "description": { "type": "string" },
        "location": { "type": "string" },
        "era": { "type": "string" }
      },
      "required": ["worldName"]
    },
    "world": {
      "type": "object",
      "description": "Deep world-building elements.",
      "properties": {
        "magicSystems": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "description": { "type": "string" },
              "rules": { "type": "string" }
            },
            "required": ["name"]
          }
        },
        "races": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "traits": {
                "type": "array",
                "items": { "type": "string" }
              },
              "culture": { "type": "string" }
            },
            "required": ["name"]
          }
        }
      }
    },
    "characters": {
      "type": "array",
      "description": "Main and supporting characters.",
      "items": {
        "type": "object",
        "properties": {
          "id": { "type": "string", "format": "uuid" },
          "name": { "type": "string" },
          "role": { "type": "string" },
          "race": { "type": "string" },
          "profession": { "type": "string" },
          "traits": {
            "type": "array",
            "items": { "type": "string" }
          },
          "arc": { "type": "string" }
        },
        "required": ["id", "name", "role"]
      }
    },
    "chapters": {
      "type": "array",
      "description": "Chapter outlines and stats.",
      "items": {
        "type": "object",
        "properties": {
          "chapterNumber": { "type": "integer", "minimum": 1 },
          "title": { "type": "string" },
          "summary": { "type": "string" },
          "wordCount": { "type": "integer", "minimum": 0 }
        },
        "required": ["chapterNumber"]
      }
    },
    "notes": {
      "type": "string",
      "description": "Freeform comments or TODOs."
    }
  },
  "required": ["projectId", "title", "author", "createdAt"],
  "additionalProperties": false
}