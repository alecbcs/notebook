# Embed PDFs into LaTex Documents
### Prepare Latex Documents
Use Inkscape to convert pdf documents and add metadata.
`inkscape -o=output.pdf --export-latex input.pdf`

### LaTex Command
Don't forget the `[H]` otherwise LaTex will decide to put the PDF where is wants not where you want.
```latex
\begin{figure}[H]
    \centering
    \def\svgwidth{\columnwidth}
    \input{output.pdf_tex}
\end{figure}
```
