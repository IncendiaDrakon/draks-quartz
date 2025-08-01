# Fake Twitter/Bluesky post embeds/previews in Obsidian

## Use this HTML template:

```html
<div class="social-card horizontal">
  <img src="/images/ladybug-post.png" alt="Ladybug ritual preview" class="card-image">
  <div class="card-body">
    <p class="card-author">@drakon</p>
    <p class="card-text">“Ladybugs logged. Render queue frozen. Audit complete.”</p>
    <p class="card-footer">
      <a href="https://bsky.app/profile/drakon.bsky.social/post/xyz" target="_blank">View on Bluesky</a>
    </p>
  </div>
</div>
```

## CSS snippet for Obsidian:

```.css
.social-card.horizontal {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  border: 1px solid var(--gray);
  border-radius: 10px;
  background-color: var(--background-secondary);
  padding: 1em;
  max-width: 700px;
  height: 200px; /* Fixed card height */
  box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
}

.card-image {
  height: 100%;
  width: auto;
  max-width: 180px; /* constrain if needed */
  object-fit: cover;
  border-radius: 8px;
  margin-right: 1em;
  flex-shrink: 0;
}

.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 1;
  overflow: hidden;
}
```

## .scss for quartz (quartz\styles\custom.scss)

```.scss
.social-card {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  border: 1px solid var(--gray);
  border-radius: 10px;
  background-color: var(--background-secondary);
  padding: 1em;
  max-width: 700px;
  height: 200px;
  box-shadow: 2px 2px 8px rgba(0,0,0,0.1);

  .card-image {
    height: 100%;
    width: auto;
    max-width: 180px;
    object-fit: cover;
    border-radius: 8px;
    margin-right: 1em;
    flex-shrink: 0;
  }

  .card-body {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    overflow: hidden;

    .card-author {
      font-weight: bold;
      font-size: 1.1em;
    }

    .card-text {
      font-style: italic;
      color: var(--text);
    }

    .card-footer a {
      color: var(--accent);
      text-decoration: none;
      font-size: 0.9em;
    }
  }
}

```
## Preview:

<div class="social-card horizontal">
  <img src="https://cdn.bsky.app/img/feed_fullsize/plain/did:plc:vigxa24owwfxyoe5nnweh7i4/bafkreifnvqsnq2rltlvglvk6svfnmi57nv65kreajpvjhgxo7fmmomh63a@jpeg" alt="Ladybug ritual preview" class="card-image">
  <div class="card-body">
    <p class="card-author">Drakon (@drakon.bsky.social)</p>
    <p class="card-text">“tha bun's chuffed”</p>
    <p class="card-footer">
      <a href="https://bsky.app/profile/drakon.bsky.social/post/3lapao7eob22f" target="_blank">View on Bluesky</a>
    </p>
  </div>
</div>
