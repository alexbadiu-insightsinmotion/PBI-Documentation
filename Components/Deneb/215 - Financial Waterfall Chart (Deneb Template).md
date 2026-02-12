<img width="1280" height="659" alt="215 - Image - Title - Financial Waterfall Chart" src="https://github.com/user-attachments/assets/23f6cb3f-cbcb-408b-bf77-58c3bd9f7464" />

## Financial Waterfall Chart

*February 10, 2026*

Deneb/Vega-Lite can be used to generate a Financial Waterfall Chart, which graphically depicts the major elements of a profit and loss statement.

*(Perhaps it's just the engineer in me, but I’ve always found P&L statements difficult to read and was interested in how Deneb could help make the comparisons more visible and insights faster to glean.)*

The example presented herein uses a ranged column chart with amount and percent data labels to increase the utility of the visual. A simple native Power BI year slicer is included.

A simple synthetic dataset representing some common P&L statistics and components was used in the preparation of this template, but actual organization data could be easily shaped into a similar format using standard Power BI methods.

I provide a Deneb template for just this scenario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "d8e1ab26-3479-40d5-a20d-05eaff3a3f41",
      "generated": "2026-02-09T18:57:02.043Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJUAAABOCAYAAAApW1SjAAAQAElEQVR4AexdCVxU1f6/9w6LoIKg+AD3FuuP2+tlmSg9tRIhNX09FJlhZsDcRdTcexVWomZYCrhgzj5AQiqQLC5JymIuLYJoPi2fua+Jss72//4mxsZlEFPKicvnfjnn/H6/8zvn/M7vnnPu7w4Dx9T9DBgwwIFQV7wjCQoKcgaRBZjBgwc3R2rOI7V5hYSECAIDAz0hwA4bNsx1+PDhLYlGgD63hupBff6yIwtwmGAXTPAcNze3ga6urq8OGTJk8tChQ0cGBweHBQcHv/EqfpCGmUymkcgOg6xQIBCEQeY5lN8D71PQxiEfhbrjUY4GqO7EGzduTILsbPCm6vX6sTqdTlJTU9OmsrIyCvqeAm8hZAPBj4KOwcDbwJt2ZD++q3exAFdeXt4K9KsGg+EJlmW7YKI9MOF9AF/Q2xiNxm4cxxlA74pyb8Abci5IGcg8jlQAlFMecu6Qb4V8L9AuonwG+dNAZ+S9ATc4FQeZdtDnDj2XIPd38ElPV6RHUC4D+MuOLcDl5eWdzcnJWbdly5bVwCfAImAeaB9lZ2cvQfrhF1988Rlo7wHvoBwH+krQ9iIVAhGgfYZ0OrAsNzd3Icpzkf8cdrnaokWL9ci/ibpvAbF17c1GfjvoS+owHXUSUDcNaQ7q8ZcdW4DD6sAmJCT0AVpbxrFy5UqvtWvXulMZeTeZTNYhPj6+B5XXrVv3t6SkpG6oxxENfGfAi3iExMTEFqjrA3TE1nY4ICDASHTIuMnl8mYxMTEOVCb+smXL6GxGxZsgPnSz4LtSnuqtXr36Geh9AmlnSm8K12UgQ+e9utJvCWQ7UF+RPvcblWFIHuPtQ6k1nc8/HAtwMLgntqXeQOiaNWuiMHEfYFuSYDscg/Jr2KZG4wzUw8HBoeuqVavG42wUVltb2w9yAagTAtm+SP0hOxYTKER5EJyiHeRGoW4E6oWjjcmQCa+urpa0bdt2Buq+TvzmzZtLoTMKmAkHjQB9goeHxxQ41FCcvwZAVop6/8ZQ20FvG6TPIH0dcqRjJNJ5cI65kBkFHVHIz0e6AOlL4I1EP15Bmz6o1xP08cAUOJIY7dJ2HIy+zYTsJMi+hfajkU4F3oSMG+rw1++0ADd16tTLkydPTiTAWZSYzPejoqI+QnnNxIkTM6ZMmbIOMtmTJk36HLQk8DUoJyH/FXjvQDYf5QzIrh8/frwWzpIHPUfB+wi0xZD7FPlVkEmEjrUoL0P6OWjUBrUbD9py6JGDvjY6OnoF6mVBPhv0T5HKQP8Ceo8j3QTaUqQfA5uAJeAvBdQ4pyXDibPAj0V5B3ibQMuaNm3adrS1HnTqcyLKqrFjx/6A8rvAYsiuhuwitL8CaQIQB5ny32lP+6vWCD2+GVIg3WRMoIbytgD+RVs8ooNfAzz0SYHOetuFc1yGQ5RSHyy4Vx2LHJ8+XAvc4lQPVzWvralawOxUiA2ZD9ojR45sjfhTx5dfftkd8SsKXPogeOmDvFPfvn1dKICJPIUQGARKW5DRiE8A/Q6ZpcP7tSQZ8FyeffZZR8rfjqKiDWYedDwBObPu22X4sn1ZgEPAsj8OvxfgWAtwqH0S55B/Ozk5iXA4H4MzypM4zAZVVVVJPD09X8PhffQvv/zyGGTbu7i4xCFo+S8ckjvdJvMG6rrFje7flW3BfrQkLCAQsbBBbdu2nYC2xsBpp+CpcCYcyOVQweYJbibnT17y9/8b2nqpoqJiJnRPhUw0pSRjX+bke0sW4OAQ5+FU+XCOk4gR7cETUyKQgTiSBjGkXUhliElRHCsVZfm2bdv+i4p0ZjoKJ7tCdW6TWYnyVYPRodzEMkcdWO4KYlNbIEdxqBToSoSe5WlpaVUsJzhvNDElH8bHnzp//rwMT2UJJAeZFZSSDNriLzuzAIcJ/C+cYCCgob5jMmuAU5S3BfDLgTgEK/NtycxJyz83V1sQN0v71T5bMn7+wzb37P9aAvEPHDig452ILGH/MJ+p7H8YTWUE9jFO3qnsY57sqpe/y6nWrVvXBdFpCaLofohE90NU+pbXPHZlAb6zD90Cv8upEFV/BYf5AES5/XHQfxmH/HDA/I7vofeQV2h3FvhdToXXG0l49fEGotifIoq9EOWpwFW7Gz3f4UaxwO9yKrwg7oDtbyZevkqBt/AC9q6fEmiUHvNKH3kL3JdTfSjsN3pZWEBoZWFqv4qClDM3didXA8dr9qSNJPrSsH7/ohEjcLly1qxZqh07duzduXPn/qKiom9VKlVuVlbWruXLl28Ef8GRgoyWpYUZofXh4K6N/yR9POzLAvflVIyJHWRiTANtgWXYwMGDB3dAMDXqp59+Cnd0dHzOw8PjWZy7/u7l5RXYvn37gLNnz44E/00da2wLUw2sFyz7FPj2ejXZft+XU7EsY6rPUhzL/MLU/eDVDoOViTl8+DBDebyqYTIzM5lDhw6RBP0xBKU8/oIWuC+nut/xY5ViunfvzlDauXNnxs/Pz6JijyVTbyrg3y/Xa59HlNmoTlVQUMDMnTuXmTdvHrNw4UJGLpffNEOPfiOPX6x1m0LYc/hibEHJWe3ug2dSCIWl5xYRvaf/8CS8hH4OL6DxbJD4xZ49e77HGW0fXi0VKBSKrVj5CvD0qaQX2yWFWYNLCzcn1ouCDNpub/aBzzSOBRrVqe7V5YEDB+oJiHt1QdzrdaPRSAdzCeo5Eh2p+QLPwdXV1aVNmzYeOKc5eXp6uj/99NO+WP3+duLEiWrU41jWwDIM61AfWPww/E+jW+BPdSrL6AwGQwny38N5rsFB1k+YMOE4yrdcGzZsOJadnU2f7GSdnJwEx44du7hq1aqvbxHiC4+EBR4Jp0IQlT4KLEP6CYKqBbYs4+Pj0xLwcHd3b4GzWjvkXW3J8vQ/zwKPhFM1dPgymawMjpc9bdq0nPnz5+/EGavez603VC/J8Xh4FrArp3p4w+Y1NaYFeKdqTOs2Ud28UzXRiW/MYfNO1ZjWbaK6eadqohPfmMP+yzhVd/8ReWyrmqjjly7NKi47m77n8NlNiNJn7P3h3NristNy4nXrN/zLoKCg0UA8Iv3anJycQkTo92q12m2Izu+Oi4vbRLyhQ4f2KinImFhakBFvC4eKMtcc2r2hY2NOjr3qtk+nsmHtbt1G1V64YHStrTU8o9OZBiOY2rOqSi/S6ZgOxKNqCKrTmJ18fX1b9ezZ8/GuXbt2euyxx7x79OjRpba21swzGo0sy5kEDMs42QJ0I4LfjFTyuM0CnHUZL9j+b/Xq1aPi4+MHAHb52fNx48adh1MUYtK3IaXvhdg4efLkNOtxUj43N/cUIvQHjx49ehZyJqxapbt27TpHPB4PZoFbnAp3cQhemQzA+7X+Dg4OdvvZ86ioqEI4Ug6i8x8DNiP0zs7ODlix3Dt16tTWz8/P+8FMyde2WOAWp8JEvIeI9eSJEyd+gLf/f/nPnqekpPx3+vTpW7G6ZSxdupR/j2jxigdMb3GqhISE1tgC6YvIhmMbnIFyV2v9JhNOGNaE2/JGE0PfH8rwP03bAmanWhrab/iHYf1DKotSB1UUplTcKEh2vr5bewrlXkQnkJlwMk2rFxyTQnI8mrYFzE7FcuyrMMPL9SEmJoabnVywvV5oCvKhg7+auAV+dSoTe7nx7MBrbmoWMDtVUxt0Q8ZLoaqGyPEyd1qAd6o7bWKm9Nj+7aqLtVeiDxz7ZdGew+cyvz5yLhVR+g1Fh06nFZedXEK8bgHDTyLyPv9QYeYKWygp2Lzy0M4N5m8dNCtuAr94p7IxyWxMjHHgwIjqioqKTjU1+h41NYYAoL/BwAqNRieOeFQVDy4OJsbUzBYQ+2tyf73NOxV5Rj0wmUzfchy3F0HhrxF5p2j9XT9DX4+KJsfineoeU46I/A0Egr9ElD4PWINywT2qNHk271RN3gUevgFud6qH3wKvsclZgHeqJjfljT9g3qka38ZNrgXeqZrclDf+gHmnelAb8xa8w4K8Se4wyf0Rqp24uOor3IySo1cWF5Sc3XbgyKXNxWUXPiv6/nTyd2UX3idet4GjbpQWZiwtLcr42BYQeV92fy0/utK8Uz3g3PTuPayy97BhlVerqjogOPp8ZW1tX71eH6BnmJByna6CeOYmTIwTY2JcbYFl2EfjA+/mzj7YL96pHsx+N2tT5B2vZHIReS9F/gocbOXkyZOb5Dc280510y0eLINIuznyPnXq1A1wpnikRx9Mo/3W5p3Kfufuke0571SP7NTYb8d4p/qD5q66GfeW4ca1maXHL8bvP3Lp831HL2TsKTm7ofjgyZSSH0594NmMmxsUFOQcHBy8nCCTybKKi4sPpKenb6N8RkbGl0QH/rN/1+c+5r+cLspcXno3FGasLd29ecofNLQ7muGd6g6TNA6BnhJ7BYorLl+vcamoru5ZXa1/Xmcy9deZBP++Ws3e8MVTZFVVFYtDfnNC+/btvVu1auXp4uLi1qdPHz9PT8/WRAccOc4BD4v0NGlqzpjuAgzBJKDvP0XmT7h4p/qDjc6y7DFgH5zjGzRdbuspcePGjT+UlZWdhmO5njx58vKmTZsOQ/6269Es8k71B88LngyvAl8BmZMmTfrY1lPik08+6f7UU095d+jQoU2XLl282rVr19zS1X/0f+0MazCtIJy6dCO17MTlAz+cuFJA+PlCeQrROQO7aciQIZ2xXUaHh4fPyc/P31RYWLglMzNTu3Pnzk0ajSaJeNhyg0p3b+xVUpjxbklRRvTdcLAw4/2Sos3+lvbvlfJOdS8L/Un87du3n5k9e/aOCRMmZM6YMWMrla270u3FEWWEH09f63zpWnWHC+XVjwGDTl6o/Jno9Pl5gUDQAiuin4+PT293d3c/bKVPdOzY8Xk46XM6ne5x4mHVbMM6cjrsp9Ucw1Zfr9S7nrtc0e7MhYp2Zy/d8KmpNghYxlTN6U36Oid9Hc5oEwMGDGjGWXeUz9ufBbB9ZqLXB5DSVnrXjzqXlJRcxXZaevHixfLKysqaoqKi46Dd/BLebi+MKOveb/jSbv7D13539Py+H/535Zcfz167duzUtRZ7j5yT9+g3YlG3F0fuhQO+gbbSsWqmh4aGpo8bNy4dTpQ+YsSI9F69eqUTz9XVNZR3KljCni9sn5exlW5G8LXeLyPB2czJ19fXo3Xr1i3gAO3hGDe3U+vxQ9d26IzF1rwI+anAHW8FsPIxL7zwAtO7d28mJCSECQwMZJo3/00d71TWFv0L52n7nDNnzo7p06fnzZo1C8XtZ+423NWrV7ddsWKFf2Ji4nsJCQm3fJeGRX7//v0MQh0MVjvm9OnTzLFjx5hLly5Z2AzvVDdNwWfIAlihLkRHRxdh5XsHK5bNV030f4fgdExsbCwTFxfHHD36myjvVGTJPwZNppU/y6leaDIWboID/dWpONMf/U8d+a9B/As7m9mpOIZNYxhTRn2IiYkxNsQOW7du/RmPnv+5B95tiC6SQSzlOJBRHxwcmwFvXwAABsdJREFUHOi/a5H4PYF+ldSnq4734z0VNYIAApTVde3bHC/HcfkNbVqn0/10L30IRXzfUH2w3Vag3rlFe7s5UvimdveOOcmF2aUOj39fIugoKBE8xnzHdLpxQuf7DdEJDH7EYnE7RGdDxWLhUHFo6DMSkeh1kUj0SqRwdJBEInl2/PgQd4gxW7ZsWbRly5ZYL69WW33c3D5FnsrWSCI5wvjx412lUuFzYWFhL46VSF6F/v4WPcTPy8u7kpubm03Ao+y+dp6ehxwdHfMRcd5BNEJWVtYRkiVERka2jBCJ/EWhof7oWy/0uW9UVNTN7zNAX0qpDuny9fK6gGDgNipbIycnp5x0EVC/nVQqGhEeHhYYER7eB329Y+seGxbWSSoNHRAREeofGRneH+2+QnIE0mEBxtZRKg0f9mvfxgwZFyHyl0hEo6jPFpn2rVsf9Pb2+NG6P+hjvqenZzHR0P+dFllKRaJQ/4gI0T/E4pC+aLt3RESEF9EJuMErfH1bfefl5XWY6hK8vb2LWrZsmUf5Ohwk2fDw8ObhYWGBY8Vhz4eHjxkUETH6H0Kh8AWpNCwYYQMXksnOzt6F9s3z2LZt2yRvd3cN4lIrgGUWOmx33OxUVIGgUqlOq9UpWWq1Ojs5OXnXqrS0W7apX/nqVJVK+4UqNfXbLqdOZTxx6tROmfazHKVSeSApKe0a6SHAMdxMJq5vraNgrCRcGCsVCxdLw4XjiGeNpKSkSoVCu4/aW69UbkHbBdZ6rGVZvf4pvYB7z6u1x9vXr1153ZpnyeON/nW5RlOkSU0twquI79Hn4vj4ePqWYouIOSVdJo4JrqmpjJaIRfESiXCKWBz2vJlp9Qv1TysUms1qdXKeXK3+WqHQ3vGvetcnJ/9PoUjNl8tTi2QydQHa3UZyBCtVDMZ2UqFQZ/3at5TcdXJNkVKp2UB9tsjpHdnurIEbExEu/CBCKvokQiKZo6upmuXoKBgnkaCfeOVikaVUo0ktkss136hUacVoe79cLr9IdAuMRoeuHGMYJpGELwSmcEbj281dnBdLJeEfY17etDgM+lahTk7OW69K3qtWp3wpl3/2jVar3aNQJGenpaVVWfRZUrKf0UEQ6+ba7D0XR8cXLXRKb3EqItwPYvLz9YTb61BH9VXNnqysrF6jUmlilWrtAoVKO1+h1q67XbYh5cjIUN8IodBPplYXKNUaiUyhmg99ybfXxd3WMVIsHog77Z9YLQZIpWOelkiEL0WEhb1mvRqY6znqfmT0xnRM6kcmhlvi7OyQW1WlO2Dm1f2iFU4iFPaLjBQHicXCIOgPjpQIB0O3T50IA1pzrNi0wg4C/RWJMPQlWo0iI8f0lYaGBuBub0+y1Jc3pGPAFxI/eKxINASrSqDUvNILR0aEhnYgOYVCk2sSOK42GpkcvYF9S65ULjOY9JtdXVusc641LBQ4GihyTaIMxtoX9YdglxhMbaH9XlKpKID6bRbAL+jLFzga0zm98TOTiU3VM0xsS3ePtwVGZr2zS/OVd3MYVLN5YWdxlEql3jQXcpVauF6pnqlKTt5uXeGBnMpakXUe75g8sQqEuDo5vIM77n2pWLQEd0WsWCRaECEJnz92bMh9PRjQ3WZi2VHQ8y6MmAhd85HHXSyKgL4Z5MTUvlqtPilTqXbiTvsKq0W+QpFyRKnU7pAnJ2dYrwYky+id/EwCdoRUKp4pYNlpuir9KDdHR7MDEJ9AK5xSqy2UyVQ5KpU2B/qzr1fW7qipqblMfAJoFUqNhlbYL9Hmti6nz33V+cTPOTJZSrEiNXU37vZTJEd9+VSRsg36dmC1yl6v0eRiVclTaDTbZFrtJnlq6s8kR+A4roIVsP05jpGKscoLBA6hldevj0hKSbkkkyXfPO9hrMUGlt3NGAyOjKOjl4ODkYUT7aZ+kx4LzPYTsNOwSk2ATsn161cXGjnDCIPhakuLTENTvV7fjGGMIRJaNSWiWdh95knFok8wz0st89ooTkVbhlypnqvUpvxHrta+rVBp5inV2gUqjSYW9MXr16ddaeggSA6GyofxY6BnIdIp0LUY+elypUYOfR/f791GOjEh26EjVqFQLcdqMBf9XEzbGPHqA9oyALW2ZGjlJtjiN4RONwD6tlSpVCeq1Nr5crl6ARz3t/9qbqXE4tQKtXqjQpH8nRWLEYvFremGM9tPpZkI25nH27Klx7uMgftSIGAM1vINyZv7plDFK5WaKOAjhVq7BH2dDvvNtcxrozhVQzrHyzS+BQQCU3cXZ6eF2J5nYUV/R0rnWrEo8frVq0GsQNBGV9NsNugfYDtr9TB78/8AAAD//y7b5/4AAAAGSURBVAMARYRgCw67whIAAAAASUVORK5CYII=",
      "name": "Financial Waterfall Chart",
      "description": "A graphical profit and loss chart to present P&L components visually and speed insights.",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.8.2.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "6.4.1"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  \"legend\": {\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelFontWeight\": \"normal\",\r\n    \"labelFontStyle\": \"italic\",\r\n    \"labelColor\": \"#4A4A4A\",\r\n    \"symbolSize\": 200,\r\n    \"symbolType\": \"circle\"\r\n  },\r\n  \"axis\": {\r\n    \"ticks\": false,\r\n    \"grid\": false,\r\n    \"domain\": false,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelFontWeight\": \"normal\",\r\n    \"labelColor\": \"#605E5C\"\r\n  },\r\n  \"axisX\": {\r\n    \"labelAngle\": 0,\r\n    \"labelPadding\": 5,\r\n    // extract the name from the X-axis composite label/\r\n    // compose an array to allow the name to be rendered on multiple lines\r\n    \"labelExpr\": \"split( slice( datum.value, 5, 100 ), '|' )\",\r\n    // use different font sizes (accentuate the major items)\r\n    \"labelFontSize\": {\r\n      \"expr\": \"slice( datum.value, 3, 4 ) == 'S' ? 14 : 10\"\r\n    },\r\n    // use different font weights (accentuate the major items)            \r\n    \"labelFontWeight\": {\r\n      \"expr\": \"slice( datum.value, 3, 4 ) == 'S' ? 'bold' : 'normal'\"\r\n    }\r\n  },\r\n  \"style\": {\r\n    \"_column_style\": {\r\n      \"cornerRadius\": 4\r\n    },\r\n    \"_statistic_amount_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 16,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#FFFFFF\"\r\n    },\r\n    \"_statistic_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#FFFFFF\"\r\n    },\r\n    \"_amount_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 10,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__1__",
        "name": "Item",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "Item with Delimiter",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__3__",
        "name": "Type",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__4__",
        "name": "Year",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__5__",
        "name": "Amount",
        "description": "",
        "kind": "column",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 10,
    "text": "Financial Waterfall Chart",
    "subtitle": "Graphical Profit & Loss | Absolute Amounts in € | Percentages of Gross Revenue"
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_id"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_item"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_item_with_delimiter"
    },
    {
      "calculate": "datum['__5__']",
      "as": "_amount"
    },
    {
      "calculate": "datum['__4__']",
      "as": "_year"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_type"
    },
    // compose a composite label for the X-axis
    {
      "calculate": "pad( datum['__0__'], 2, '0', 'left' ) + '-' + slice( datum['__3__'], 0, 1 ) + '-' + datum['__2__']",
      "as": "_item_id_type_name"
    },
    {
      "calculate": "datum['__3__'] == 'Income' ? datum['__5__'] : datum['__3__'] == 'Expense' ? -1 * datum['__5__'] : 0",
      "as": "_increment_amount"
    },
    {
      "window": [
        {
          "op": "sum",
          "field": "_increment_amount",
          "as": "_top_amount"
        }
      ],
      "sort": [
        {
          "field": "__0__",
          "order": "ascending"
        }
      ],
      "frame": [
        null,
        0
      ]
    },
    {
      "calculate": "datum['__3__'] == 'Statistic' ? 0 : datum['_top_amount'] - datum['_increment_amount']",
      "as": "_bottom_amount"
    },
    {
      "calculate": "datum['__1__'] == 'Gross Revenue' ? datum['__5__'] : 0",
      "as": "_gross_revenue"
    },
    {
      "calculate": "datum['__1__'] == 'Net Revenue' ? datum['__5__'] : 0",
      "as": "_net_revenue"
    },
    {
      "calculate": "datum['__1__'] == 'Gross Profit' ? datum['__5__'] : 0",
      "as": "_gross_profit"
    },
    {
      "calculate": "datum['__1__'] == 'Operating Profit' ? datum['__5__'] : 0",
      "as": "_operating_profit"
    },
    {
      "calculate": "datum['__1__'] == 'Earnings Before Income Tax' ? datum['__5__'] : 0",
      "as": "_earnings_before_income_tax"
    },
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "_gross_revenue",
          "as": "_gross_revenue_amount"
        },
        {
          "op": "sum",
          "field": "_net_revenue",
          "as": "_net_revenue_amount"
        },
        {
          "op": "sum",
          "field": "_gross_profit",
          "as": "_gross_profit_amount"
        },
        {
          "op": "sum",
          "field": "_operating_profit",
          "as": "_operating_profit_amount"
        },
        {
          "op": "sum",
          "field": "_earnings_before_income_tax",
          "as": "_earnings_before_income_tax_amount"
        }
      ]
    },
    {
      "calculate": "datum['__5__'] / datum['_gross_revenue_amount']",
      "as": "_percent_of_gross_revenue"
    }
  ],
  "spacing": 0,
  "vconcat": [
    {
      "name": "LEGEND",
      "width": 1180,
      "height": 1,
      "data": {
        "values": [
          {
            "legend_id": 1,
            "legend_size": 2,
            "legend_label": "Major Statistic"
          },
          {
            "legend_id": 2,
            "legend_size": 2,
            "legend_label": "Statistic"
          },
          {
            "legend_id": 3,
            "legend_size": 1,
            "legend_label": "Income"
          },
          {
            "legend_id": 4,
            "legend_size": 1,
            "legend_label": "Expense"
          }
        ]
      },
      "mark": {
        "type": "arc",
        "radius": 0
      },
      "encoding": {
        "theta": {
          "field": "legend_size",
          "type": "quantitative"
        },
        "color": {
          "field": "legend_label",
          "type": "nominal",
          "scale": {
            "domain": [
              "Major Statistic",
              "Statistic",
              "Income",
              "Expense"
            ],
            "range": [
              "#4A4A4A",
              "#4A4A4A", // opacity set to 60% below
              {
                "expr": "pbiColor('positive')"
              },
              {
                "expr": "pbiColor('negative')"
              }
            ]
          },
          "legend": {
            "direction": "horizontal",
            "title": null,
            "orient": "none",
            "legendY": 20,
            // set the opacity to 60% for all but "Major Statistic", which is set to 100%
            "symbolOpacity": {
              "expr": "datum.value == 'Major Statistic' ? 1 : 0.6"
            }
          }
        }
      }
    },
    {
      "name": "WATERFALL",
      "width": 1180,
      "height": 510,
      "encoding": {
        "x": {
          "field": "_item_id_type_name",
          "type": "nominal",
          "axis": {
            "title": null
          }
        },
        "y": {
          "field": "_top_amount",
          "type": "quantitative",
          "axis": null,
          // adjust scale to suit dataset
          "scale": {
            "domain": [
              0,
              160000
            ]
          }
        },
        "y2": {
          "field": "_bottom_amount"
        }
      },
      "layer": [
        {
          "name": "COLUMN_CHART",
          "mark": {
            "type": "bar",
            "opacity": 0.9,
            "style": "_column_style"
          },
          "encoding": {
            "color": {
              "condition": [
                {
                  "test": "datum['__3__'] == 'Statistic'",
                  "value": "#4A4A4A"
                },
                {
                  "test": "datum['__3__'] == 'Income'",
                  "value": {
                    "expr": "pbiColor('positive')"
                  }
                },
                {
                  "test": "datum['__3__'] == 'Expense'",
                  "value": {
                    "expr": "pbiColor('negative')"
                  }
                }
              ],
              "value": "transparent"
            },
            "opacity": {
              "condition": [
                {
                  "test": "datum['__3__'] == 'Statistic' && ( datum['__1__'] == 'Gross Revenue' || datum['__1__'] == 'Net Income' )",
                  "value": 1
                }
              ],
              "value": 0.6
            }
          }
        },
        {
          "name": "STATISTIC_AMOUNT_LABELS",
          "transform": [
            {
              "filter": "datum['_type'] == 'Statistic'"
            }
          ],
          "mark": {
            "type": "text",
            "yOffset": 10,
            "style": "_statistic_amount_text_style"
          },
          "encoding": {
            "text": {
              "field": "_amount",
              "formatType": "pbiFormat",
              "format": "0,. K"
            }
          }
        },
        {
          "name": "STATISTIC_PERCENT_LABELS",
          "transform": [
            {
              "filter": "datum['_type'] == 'Statistic'"
            }
          ],
          "mark": {
            "type": "text",
            "yOffset": 24,
            "style": "_statistic_percent_text_style"
          },
          "encoding": {
            "text": {
              "field": "_percent_of_gross_revenue",
              "formatType": "pbiFormat",
              "format": "0.%"
            }
          }
        },
        {
          "name": "AMOUNT_LABELS",
          "transform": [
            {
              "filter": "datum['_type'] != 'Statistic'"
            }
          ],
          "mark": {
            "type": "text",
            "yOffset": {
              "expr": "datum['_type'] == 'Income' ? -22 : 10"
            },
            "style": "_amount_text_style"
          },
          "encoding": {
            "text": {
              "field": "_amount",
              "formatType": "pbiFormat",
              "format": "#,.0 K"
            }
          }
        },
        {
          "name": "PERCENT_LABELS",
          "transform": [
            {
              "filter": "datum['_type'] != 'Statistic'"
            }
          ],
          "mark": {
            "type": "text",
            "yOffset": {
              "expr": "datum['_type'] == 'Income' ? -10 : 22"
            },
            "style": "_percent_text_style"
          },
          "encoding": {
            "text": {
              "field": "_percent_of_gross_revenue",
              "formatType": "pbiFormat",
              "format": "0.0%"
            }
          }
        }
      ]
    }
  ]
}
```

</details>

<br>
This example illustrates a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with ***subtitle***
- a standard Power BI dataset
- a shared ***transform*** block with:
    - 6x ***calculate*** transforms to assign internal names to the Power BI dataset fields- 
    - a ***calculate*** transform to set a composite item identifier (id, type, delimited name) to ease sorting and to make the id, type, and delimited name available for axis processing
    - a ***calculate*** transform to determine the signed increment amount
    - a ***window/sum*** transform to determine the cumulative amount for the range top amount
    - a ***calculate*** transform to determine the range bottom amount (statistic = 0)
    - 5x ***calculate*** transforms and 5x ***joinaggregate/sum*** transforms to determine the statistic amounts
    - a ***calculate*** transform to determine the percentage
- a ***vconcat*** block for the custom legend and column chart

1 - Legend:
- a 4-record in-line dataset (major statistic, statistic, income, expense)
- an ***arc*** mark of zero radius to leverage the legend functionality built-in to Vega-Lite
- a ***color*** encoding with:
    - a hard-coded scale (domain and range) for the colours
    - ***conditional symbol opacity*** (major statistic 100%, others 60%)

2 - Waterfall:
- a shared ***encoding*** block to ensure all marks use the same X and Y axes and scales
- the X axis configured with:
    - ***multi-line labels*** for the items (extract the name from the composite identifier and split into an array using the delimiter)
    - ***conditional font size*** (statistic larger)
    - ***conditional font weight*** (statistic bold)
- the Y axis configured with:
    - both a Y (top) and Y2 (bottom) to create an amount range
- a ***layer*** block for the columns and labels

2a - Column
- a ***bar*** mark with:
    - rounded corners (4px)
    - ***conditional colour*** for the columns (statistic=grey, income and expense set to the positive and negative ***Power BI theme sentiment colours***)
    - ***conditional opacity*** for the columns (major statistic=100%, others 60%)
    - a *named style*

2b - Statistic Amount Label:
- a ***text*** mark with:
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - larger font size, bold weight, and white colour
    - a *named style*

2c - Statistic Percent Label:
- a ***text*** mark with:
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - smaller font size, normal weight, and white colour
    - a *named style*

2d - Component Amount Label:
- a ***text*** mark with:
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - larger font size, bold weight, and dark grey colour
    - ***conditional Y offset*** (income above, expense below)
    - a *named style*
  
2e - Component Percent Label:
- a ***text*** mark with:
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - smaller font size, normal weight, and dark grey colour
    - ***conditional Y offset*** (income above, expense below) 
    - a *named style*

3 - Config:
- configuration values set for:
    - border (colour [stroke] set to null)
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
    - legend attributes (font family, size, weight, style, colour; symbol type, size)
    - general ***axis*** attributes (ticks [disabled], grid [disabled], domain [disabled], label font attributes [family, size, weight, colour])
    - ***X*** axis attributes with:
        - a ***label expression*** to extract the name from the composite item identifier and split into an array using the delimiter
        - ***conditional font size*** (statistic larger, component smaller)
        - ***conditional font weight*** (statistic bold, component normal)
    - named styles:
        - bar/column (rounded corners)
        - statistic amount text attributes (family, size, weight, style, colour)
        - statistic percent text attributes (family, size, weight, style, colour)
        - component amount text attributes (family, size, weight, style, colour)
        - component percent text attributes (family, size, weight, style, colour)

<hr>

### Links:

Here's the template:

[915.1 - JSON - Deneb Template - Financial Waterfall Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/914.1%20-%20deneb_correlation_chart.v1.8.2.json) <br> *** FIX ***

<br>

Here's an example Power BI file using the template:

[915.2 - PBIX - Deneb Example - Financial Waterfall Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/914.2%20-%20Deneb%20Reusable%20Components%20-%20Correlation%20Chart%20-%20V1.8.2.pbix) <br> *** FIX ***

*- eof*
