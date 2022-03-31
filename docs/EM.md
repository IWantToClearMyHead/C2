- color

```diff
- text in red
+ text in green
! text in orange
# text in gray
```

- jump

<a href="#top">Back to top</a>

- checkbox

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

- yes and no

✅ &#9745;
❌ &#9746;

- diagram
```mermaid
stateDiagram-v2
  [*] --> Unwritten
  
  Unwritten --> Open: Open
  Unwritten --> Void: Void
  
  Open --> Void: Void
  Open --> Cancelled: Cancel
  Open --> Closed: Close
  Open --> Open: Update
  
  Closed --> Open: Open
```

- graphviz
```graphviz
digraph PolicyState {
  size="8,5"
  node [shape = doublecircle]; Unwritten;
  node [shape = rectangle style=filled]; Void Cancelled;
  node [shape = circle];
  Unwritten -> Open [ label = "Open" ];
  Unwritten -> Void[ label = "Void" ];
  Open -> Cancelled [ label = "Cancel" ];
  Open -> Closed [label = "Close" ];
  Open -> Open [label = "Update"];
  Open -> Void [label = "Void"];
  Closed -> Open [label = "Open"];
  Void [color="0.000 1.000 1.000"];
  Cancelled [color="0.201 0.753 1.000"];
}
```
<a href="index.md">Back to home</a>
