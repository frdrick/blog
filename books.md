---
layout: default
title: books
---

## Books I've read

<input type="text" id="searchInput"  placeholder="Search" title="Type in a name">
<table class = "sortable" id="myTable">
	<thead>
	<tr class="header">
		<th>Title</th>
		<th>Author</th>
		<th>Stars</th>
		<th>Date Read</th>
		<th class="no-sort">ISBN</th>
	</tr>
	</thead>
	<tbody>
	{% for k in site.data.books %}
	<tr>
		<td><a href="/books/{{k.id}}.html">{{k.Title}}</a></td>
		<td>{{k.Author}}</td>
		<td>{{k.Stars}}</td>
		<td>{{k.Finished}}</td>
		<td>{{k.ISBN}}</td>
	</tr>
	{% endfor %}
	</tbody>
</table>

<!--Add sortable table javascript and css-->
<!--<link href="https://cdn.jsdelivr.net/gh/tofsjonas/sortable@latest/dist/sortable.min.css" rel="stylesheet" />-->
<script>
document.addEventListener("click", function(d) {
    try {
        var A = d.shiftKey || d.altKey,
            f = function k(a, l) {
                return a.nodeName === l ? a : k(a.parentNode, l)
            }(d.target, "TH"),
            v = f.parentNode,
            w = v.parentNode,
            g = w.parentNode;
        if ("THEAD" === w.nodeName && g.classList.contains("sortable") && !f.classList.contains("no-sort")) {
            var h = v.cells;
            for (d = 0; d < h.length; d++) h[d] !== f && h[d].removeAttribute("aria-sort");
            h = "descending";
            ("descending" === f.getAttribute("aria-sort") || g.classList.contains("asc") && "ascending" !== f.getAttribute("aria-sort")) &&
            (h = "ascending");
            f.setAttribute("aria-sort", h);
            g.dataset.timer && clearTimeout(+g.dataset.timer);
            g.dataset.timer = setTimeout(function() {
                (function(a, l) {
                    function k(b) {
                        if (b) {
                            if (l && b.dataset.sortAlt) return b.dataset.sortAlt;
                            if (b.dataset.sort) return b.dataset.sort;
                            if (b.textContent) return b.textContent
                        }
                        return ""
                    }
                    a.dispatchEvent(new Event("sort-start", {
                        bubbles: !0
                    }));
                    for (var p = a.tHead.querySelector("th[aria-sort]"), q = a.tHead.children[0], B = "ascending" === p.getAttribute("aria-sort"), C = a.classList.contains("n-last"),
                            y = function(b, m, c) {
                                var e = k(m.cells[c]),
                                    n = k(b.cells[c]);
                                if (C) {
                                    if ("" === e && "" !== n) return -1;
                                    if ("" === n && "" !== e) return 1
                                }
                                var x = +e - +n;
                                e = isNaN(x) ? e.localeCompare(n) : x;
                                return 0 === e && q.cells[c] && q.cells[c].hasAttribute("data-sort-tbr") ? y(b, m, +q.cells[c].dataset.sortTbr) : B ? -e : e
                            }, r = 0; r < a.tBodies.length; r++) {
                        var t = a.tBodies[r],
                            z = [].slice.call(t.rows, 0);
                        z.sort(function(b, m) {
                            var c;
                            return y(b, m, +(null !== (c = p.dataset.sortCol) && void 0 !== c ? c : p.cellIndex))
                        });
                        var u = t.cloneNode();
                        u.append.apply(u, z);
                        a.replaceChild(u, t)
                    }
                    a.dispatchEvent(new Event("sort-end", {
                        bubbles: !0
                    }))
                })(g, A)
            }, 1).toString()
        }
    } catch {}
});
</script>

<!--javascript for searching through the table-->
<script>
// keyup triggers when a key is released
document.getElementById('searchInput').addEventListener('keyup', function() {
//convert whatever the user searches to lowercase
  const query = this.value.toLowerCase(); // stores rows within the myTable id, tbody tags and tr
  const rows = document.querySelectorAll('#myTable tbody tr');

  rows.forEach(row => { const text = row.textContent.toLowerCase();
    row.style.display = text.includes(query) ? '' : "none";
  });
});
</script>
