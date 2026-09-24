# Profundidade com Ponto de Fuga (Java / AWT)

Projeto de Computação Gráfica (Aula 5, "Vendo 3D", Foley e Van Dam) que renderiza uma cena 3D em wireframe com projeções paralela, oblíqua e **perspectiva com ponto de fuga**.

## Como a profundidade funciona
Centro de projeção em `(0,0,-d)` e plano de projeção em `z=0`:

```
xp = d·x / (z+d)      yp = d·y / (z+d)
```

Implementado em `Mat4x4.setPerspectiveProjection(d)` (`mat[3][2] = 1/d`) seguido da divisão por `w`. Objetos mais distantes ficam menores e linhas paralelas ao eixo Z convergem para o **ponto de fuga**, posicionado no centro da janela (translada o centro para a origem, projeta e traz de volta). Arestas atrás do centro de projeção (`w < 0,1`) são recortadas. Girando a cena (Q/E), a perspectiva de um ponto vira de dois pontos.

## Controles
| Tecla | Ação |
|---|---|
| 1 / 2 / 3 | Paralela / Cavalier / Cabinet |
| 4 | Perspectiva (ponto de fuga) |
| R / F | Aproxima / afasta o centro de projeção (`d`) |
| V | Mostra/oculta ponto e linhas de fuga |
| WASD | Move a cena |
| Q / E | Gira em Y |
| Z / X | Escala |
| Espaço | Reinicia a cena |
| Mouse | Botão esquerdo: 3 cliques criam um triângulo |

## Executar
```bash
javac -encoding UTF-8 -d bin src/core2d/*.java src/core3d/*.java src/*.java
java -cp bin MainClass
```
Execute a partir da raiz do projeto (as imagens são lidas do diretório atual).
