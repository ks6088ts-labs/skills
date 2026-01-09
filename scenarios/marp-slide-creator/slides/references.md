---
marp: true
theme: custom
paginate: true
title: Reference Slides
description: Reference Slides
---

<!-- _class: title　-->
<!-- _paginate: false -->

![logo w:400px](https://avatars.githubusercontent.com/u/1254960?v=4)

# ${TITLE}

YYYY/MM/DD ks6088ts

---

# References

- [Marp](https://marp.app/)
  - [【AIスライド作成】クラスメソッド社内用のMarpテーマを作ってみた！](https://dev.classmethod.jp/articles/classmethod-marp-theme/)
  - [classmethod/classmethod-marp-theme](https://github.com/classmethod/classmethod-marp-theme)
- [Mermaid](https://mermaid.js.org/)
  - [Marpでmermaidは簡単だときいたけど](https://speakerdeck.com/eiel/marpdemermaidhajian-dan-datokiitakedo)
  - [Mermaid > Examples](https://mermaid.js.org/syntax/examples.html)

---

# Mermaid Sample

<script type="module">
import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@latest/dist/mermaid.esm.min.mjs';
mermaid.initialize({
  startOnLoad: true
});
</script>

<pre class="mermaid">
sequenceDiagram
    loop Daily query
        Alice->>Bob: Hello Bob, how are you?
        alt is sick
            Bob->>Alice: Not so good :(
        else is well
            Bob->>Alice: Feeling fresh like a daisy
        end

        opt Extra response
            Bob->>Alice: Thanks for asking
        end
    end
</pre>
