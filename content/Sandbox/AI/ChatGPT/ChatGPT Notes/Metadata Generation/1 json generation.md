You are a JSON generator. You must follow this JSON Schema exactly and return only a single JSON object—no explanations, no markdown wrappers, no extra fields.

{
  "title": "Fantasy Creative Writing Project",
  "description": "Metadata schema for organizing a fantasy story’s drafts, world-building, characters, and chapters.",
  "type": "object",
  "properties": {
    "projectId":       { "type": "string", "format": "uuid" },
    "title":           { "type": "string", "minLength": 1 },
    "author":          { "type": "string", "minLength": 1 },
    "createdAt":       { "type": "string", "format": "date-time" },
    "updatedAt":       { "type": "string", "format": "date-time" },
    "status":          { "type": "string", "enum": ["planning","drafting","revising","complete"] },
    "genre":           { "type": "string", "enum": ["fantasy"] },
    "tags":            { "type": "array", "items": { "type": "string" } },
    "setting": {
      "type": "object",
      "properties": {
        "worldName":  { "type": "string" },
        "description":{ "type": "string" },
        "location":   { "type": "string" },
        "era":        { "type": "string" }
      },
      "required": ["worldName"]
    },
    "world": {
      "type": "object",
      "properties": {
        "magicSystems": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name":        { "type": "string" },
              "description": { "type": "string" },
              "rules":       { "type": "string" }
            },
            "required": ["name"]
          }
        },
        "races": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name":    { "type": "string" },
              "traits":  { "type": "array", "items": { "type": "string" } },
              "culture": { "type": "string" }
            },
            "required": ["name"]
          }
        }
      }
    },
    "characters": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id":         { "type": "string", "format": "uuid" },
          "name":       { "type": "string" },
          "role":       { "type": "string" },
          "race":       { "type": "string" },
          "profession": { "type": "string" },
          "traits":     { "type": "array", "items": { "type": "string" } },
          "arc":        { "type": "string" }
        },
        "required": ["id","name","role"]
      }
    },
    "chapters": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "chapterNumber": { "type": "integer", "minimum": 1 },
          "title":         { "type": "string" },
          "summary":       { "type": "string" },
          "wordCount":     { "type": "integer", "minimum": 0 }
        },
        "required": ["chapterNumber"]
      }
    },
    "notes": { "type": "string" }
  },
  "required": ["projectId","title","author","createdAt"],
  "additionalProperties": false
}