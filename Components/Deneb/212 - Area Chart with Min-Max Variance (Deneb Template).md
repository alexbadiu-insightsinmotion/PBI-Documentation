<img width="1280" height="659" alt="212 - Image - Title - Area Chart with Min-Max Variance" src="https://github.com/user-attachments/assets/9ea693f4-5e30-4b61-b492-db2d3f056c2f" />

## Area Chart with Min-Max Variance

*December 10, 2025*

Deneb/Vega-Lite can be used to create an area chart enhanced with period min and max markers and variance calculations.

This example has a smoothed gradient area chart, min and max markers and labels, a min-max variance note with leader lines, and uses Power BI theme colours. All calculations are done in Deneb/Vega-Lite; no Power BI calculations (i.e., no DAX) is used. A Power BI date picker and period slicer are used as Vega-Lite does not currently provide appearance customization options.

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "bcf06df0-107c-4e90-b0ba-165df80c3f9d",
      "generated": "2025-12-10T20:54:51.647Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJUAAABPCAYAAADiB4cGAAAQAElEQVR4AexdCVxVZdp/l7Pdcze4CLikX1pamWuWk1NZTbllNqXyNYpaauGOkiCIGy6VCy6VKyCgoKaoNX2TeyKuY5Nby9TYZJmaCyjIctnuved73gvX4FzgosMoyzm/+/CcZznved7/+Z/3vPfl/IAgbdMQqGEEnKQK7N/nvqCgLnzZtocO7akPDHip/eDBfb3L+HFAQAB12RP69BFHjHjKCD4dO/4vf+7Z/M2AlxoH9esnu3KGBrzYIhDad9lMD3vtBR9nXuk5y+azuCZ1GwHCLi5G9pdyr/v2GBLQZ8zQgF5DAwf26KkUkPtY10ihvfeQgL59hw7sETA0oE93yXbzkWED+nQOHNBzWqbkeL4ox/yU6Mh51ZHh50950s9uczxYLNmeGDKg14DX+/d6THHQJygq7j60f6+hg/+314tDwIcVwctmd3S1XvcdOHRAz35Wvuj5IQN6Dxo6sHf/QQF9nmW+wIG9xzKisho0qVsIkMSUHVeSt++J2bht147klJ2rklJ2J23YundPcsquf21I2fFN8rZdm5JTPv88aevelKSUnWlJn+z5dv22nac2bNvzbvInu3clp+zYlQw5cdt3XtywddfKpE92HU6AvORtu7dt3r77JNPrt+/bmLR9d9LGLbv3JYNv3ac7f0revuuzZDguadue/0vevvtz5/7WXds3wbHMx9qKiTlRXLfg1KplCJBFUaF+i+ZOGblobsRzi2ZHvLZwXkRA9PsRXRbNDu+7ePa0Acvmh3df/N7UlxbPnfpK9OwpPZbOiRgRPTtiUPS74b2WzJn6TPS7kb0Wvxs2YuHciN7RUeHdl7A25ob1jp43ZeiyOVP/MH9eePeF88Jeh7wei+aF94ueFzFo0ezIvkvmz3h00ZzwwQvmTh4YPTuyR/S8yf/DCtKk7iNAiMB7YYquE0XJ5Hh8DdsK0h0Oe2eMlKJC3nGguMD+g8PuaIYdxVShtH2BQ9qPiNIIIdwOKcWNFMXRmmDuewUX3kAEt7UjpYgg+ggl9N9FSHmEKvgP2E5ykcPRDtnsx0Onz98UNuu9z9+JmPtd2MwFG8NnLN4aOuu9vaHTF59H2lYvECCTI98/Gxq58NPJMxecoYbcr8Kilh2YMm1RXOishXsjI9+/HhYVfS1sxoLYd2ZFfxI2/f0lU6OifgmdseCj0GnzF5f45i8PiXz/WPj0pV+Gzpy/OmzWgs9DZ8xfynxTZs5PDJsxf5HLx9qqF6jVp078F/ri/Pbnajc4+KNC176mNQTuFAGiKIpw7tw5f000DGqKAwRjXNSqVaurmmgY1BQHyj3+7nS4047TECiLgEaqsmho+zWCgEaqGoFRa6QsAs6J+oULF5ppUhcwqBs1OifqzZs3v6SJhkFNccDt8RcQECCMHjas2VuBgfcNGzasw7DXX2/z1qBB/mWHN21fQ6AqBNxIJct8+wLieMLGk84QfBxL/FOKLDwYFRUlVdWQFqseAgpC+E4E1aENeFO+2nXrNp5ITEz+VBB0uxLXr49fty45oXnzlseLi4u10ao8VLdtpaf/0sSanbE2Pztj/e1I3s306MuXf/S97RPeowPcSOWqIyYmRnvtxAVGDWrKiS9wom6IWrJy8oZczcgcwvS58xeHnL94eciV9BtDFMIN4XnhKUni6sz1qJRUNYij1lQFCFz6Zj/KufozKioqQseO/R19+Y+vUFZWFjpx8hTKyLiOCgoK0OkzZ5DD4ajg6NrtahCkevXVV73gC4iurDz33HMS2EKXLl14Jmy/1FcuD/xOm8X69OkjBgUF8bDPgV9gdrdu3ZxxsNVaB3nlznHtWgavKA5clJeFLn29H108sw8JgoC6dXsSdWjfDomSiB5q0wY1bdoYtW79IHq570tIFEXkUBRy+vQ/WVsezwF1CKXndcuFmLMmVved9gOONXmiNPGUUB/iPM9bU1JS8svKgQMHCsAuOnHiRDETtl/qK5cHfqfNYjt37ixk0wLYt4G/iNnHjh1zxsF205BX7hx+fo2KMSaKoPdCXQPnoUd6vo3sdjv6+utv0NWr6eg6jFAZGRno7NmfUHp6xi3oYd3H0alTW9aWx3NAHUWl53XLhVg+i7G677QfBoPB42O4QZAqPT29VjxDsF1pYSvMlxxAJIfdlsUEIyWr3aOPZHXu1D7riccfy3qsc8esF194NqtJYz9n3AG5BYVWP0eBrektlt3DHcASvrxWXYAbqYYPH+478vXX240YMaLpsNJ1qivnztXpb345OTm4ahjuTrRR45bHCwpy+znyc1o48nM7VE9yWtiV4ld8mrT+592psuqz6HS62yeVoii0SKDNYFhuB4xzrlMV8/j+qk9Vu6N+fn7QldpRY6Mmrb6UfZpduB2xWFp8WzuqRwhW3T2O+m5gJyYmXklK2rgbJoipZdepakun7qSO/Px8fCfHace4I3D27NnbH6lczbCJnGu/rmtfX1+NVDV0EQFLt4FI3bTHBPUB9dXW+lU9BLp27cp7ytRI5QkhLX4LgcvfHX705S6NN/774MYFMPeWbwVUOxqpVIBoZuUIZF//ZeK1cydfyc++PhqyjCAVftxIxZYUnK+7lHn1pa4vKVTY8wbiTFs9qvv+1WPH7o1958nU1Oe4tPWTHtm3Nvj54+vGtdkXO8j/q4SQ9rtXhbbbt3xcm0Mxb7cBWHBUFCKH4iaO/SJ27LQvV7zT/McdE8Qv4sMey71+8QFz4/uzMq2Og507d34Actna2eOgnwZpCeL8uJEKhjVKdELHsq++1PUlBWdPG8CP1LXjHz8YN37K3xLH9D0SN6FvWnxINPwCezovSoESti2lP7ZfgAtsH4oONKuwmEuUiPe7VnvxfFmwL5MkuhAp0toDsWO3vNAieBVHlIEIcz0LRdvCi785PuWVgvesmVdIoTUzvt/bM2edPn2avTVhQQj9GaQDyK1lJzdSsSWFxMSkFPWrL3BQnf1UZxW4rnXuH0lTHtq7Jujpg7ETJqXFTlh+KGZ8HI/JdMJzfU12XaQD06kKdnTGHF9IML5BOZoJ+10xL9qJwOdQXrhOOKk5kM5BKMmHGIVfROZRQfTBmGvpIHyexPHZmPJGnoqQIzgIobnFeTlFN2/ePIkQ+ivIDyAzQFaCpII4P26kcnrhR31aUqjOKjB0udZ+4NHksytp5IPH14V2O7oueOKhuLELiuwoRhQMSzhBepUXpNacJDcjnCwSLGVzvHCD8lKmQHVWTHjEBBHRTjkhi1Iefv8IPkwRwkIRLo0zTSFGsZhHqFDIbCaE8grYQCjeXmJzCLa2IL1AXgb5I8ijIJ1AuoCgSknFgrVWbrOwa9eueVwFvs0mayT9qzVBvLIlgG5ZEqJjDR6JG91u36qxgWlrRwceTgqJPBAzbmpafOg0nV5cI9vM8+12vEBBcn9OMD1GYBThed1VTIUckCJEeBsmlAmQiP7XBBEnZdivjHZDzZ+CHAX5DuQ0yAkQ5MxgO/VZjEajx1XgGu4/ObQhwvvg6gltD8SO65G6Mfzp45vGP34kZuKAQ3ETwg/GBS9IiwteUSSa4g7ltvi4mdkefzRuwghMpDjZoJ/Ic+ZgSnQvipK5h8RzPXlJrxclvUh18k1O4LMJLxYQShChHMhd1kRgUP0JfjwP0h2kMUi5T4MgVXVWgcuhUoFxaGWEd+qKsY0Pxo7psG91aLe0FcF/PBA/atD+mHHvpMVNCj24dtKkgzFj3zwYHxx7cO34ZKW4KJbqxDUSp1/IFTvm2xzyKl42hgg6Yx9JZ+hCTZbWVG+w8HqDTPTmRkjQjSOS0Up5/VVO1F2DRw7Mb4Q8xEvZCFMbCMIYfjGA6b3VBGpAaD9AxOZQB0FfASn3qTapWhkzm+9OCHo47aPw9vAN46lDSTM67vhwgqlca7dhrFkTJMPwgdNWTHrk0PK320RFRZHj743z2fNBcOuDWya33blq0v2pq4Lb7fhwOPuWcRstu6fm5uY6kXCPuHvWBHXhT34c3vHoupCwY2snb/p7fNjMI2tD3uUMjjheL68jOq9lskFYLJpNi3Wy/3jZ6P2abPbqa5Qsr4iGRsMlQ6NWotnPIssWSZS9sjiD6aJONmeKgukKEaVMKsg5RJDzJcwVUsQhnvAOnooFgs70G8eLedQ5+nCI1lLNEeecyh24Mh43UrF1qrcHD+6kfvWltb9XoJ73WSBZ8DIqGlcQu3WpyZsuPhI7akhq7IT7EGxfrxzjfTJ+gi/sot2rRvvtjx/z7OHYsGdObij5K3nfbRlpSY0L/svhuImz20mm5YfWhCzAOryc6I0f9br/5orixvpNeos4GxfQ1WaJW6Y3GRYa9V7LjyWMH304IXgOjAIp+1eN7sXmIewcTGBeIp/eEtIsdcOEFw/HTxx1OD74raNxIy1psZP6p64dxdZQkMFgcOsnO5ZJavJb9302P6hFasykTgcSJg199OnnU/LsdAEV9K+KFh8TNpuf5U2WJzmdt6gz+RRJkilPlIzXOUmfwQm6GxyvzyJYzLWLfB4n6bIJ4a1AlWJEqIIpRQhTGFloia4PdsmcClW1uYFNCgtlm0hk9asvVPbK1ht9iCBbrLLJ+4Js9s/TGRo354xNxnEiF5WWGPJBrtG0Lp9Iqw4khCw0ABkMOp8lnFGYVqhwCUcSJn+YV+j9gUHvHSKbfbpLXn6+ej+/jkbvJlZJ7yUKRksbfSO/QtngazSYG93UeflR3mCxSwYfXyo1Ggb+Z3Re/r6ipJ9yJLd5yqGESSNOJUzuUSwYF+VY+dUSMc6V9N5DqdEynHA+azlZN51Ssb+6839bOdj7qzVR8tF1IeOPJIZukoh5hU8T0wa90Rht1HkHSiZfzmDwKhYk0w1MBIdABCvPiVaOo/AtiEcUiEF4WqJpqQ0+p99l1+M44Tg1pG42UXvWbtx4PiEh+ajbqy+EpWIEdyAcQp0a7spiQWfMEHWWB01mv7aiyZfI3o1Fs1eTjrLZV8fL3r9BDK67r1Uw+7blzf4+nGy6hgV9LkEUESLAtxbQoj4Hvg5bkYIRIvRW+whhBHd/Hi8br2NBzuWolCP7NC6QGjURZaPvGwWCOI0aLO0NZl8iyT4ZVDJmSoLxhujtD4eZ0ikSvRBsL3f0sRwGAh5dH7HEYmiZUCTlwKPM1F9n8TdL+qZE9mqSxcte+URnKKaYUxCiqKQOjJya1cQE6nHaDTmOCCBa9afSDPU6FYEJGoHnqbtQJEomRooCjvCKM86JRU7tzKeI+QVel0+wYP/dz6GSfVqqXbZaq+JYcPAgnGjIlk3+OTBy3SScAOso5Y/jeLkIi2LL1HXzPmre2O8wrzO+LxoaddR7+1G9dzNvQbTkUWc9qvadNZdtS4uXXKdSTGCuhzxsxEP89zCADWM+Agag8rr0ribQFDwGalPc4H2/92/nLow/9+NP9yvES8dJktVZHyfYnNpZb+2tvwTn2lUfcY7Yv9Oioj1gQkVudx/HcdBHmydIdAAAB6dJREFUClKB5irxw0WjwGx6l+LZufncqW9/Nv3r3CX91z+cN57650/oSnZRAcfrESeI+dRVj1rfpfrqw/kJ5bE7O8p7CDOXL1/us3LlysTY2Fh/ZlcsLBXuGgyCQJgmpdplq/Vdjv96+bruh58vGf/961X930//YDn13b90Nkn3/R9e+NMBnSzAeoqq3rtcH7rH+NTI+dkTqWKC3PIypriMfYWFhTa2pDA8MLBt2b/6cuXcOX9CKaKUQ4SW0URl3+P4Y4+2yRk2sOelfn96Mn3cG6+dHzX45V/7vdDlErJbczFBSm2vv27UV81vf4QQs6IoN3mezyewpKDw5H73V18IEJ0ijClogjDTcKc7NS21gXDl7LsYP/jlt97b9x7133/sjOX7ny/oT37zo+nIVz94/fjzbzKqBfWV4EIRxrRW4ldSF0XYQ31wpV2DUKWasAil1EYIcS5asiWFxMSkHYLqr76w9QnIQwRGIwpSommtsZ//Y5fMgL7PXe3xTNcb7R5qndelU7vs7t06ZD3cuqW1NtZb2/Crdj0wt2acqUoIC9psNn8YqS6PGjXKymwm6iUFjCAVA5MJRXCrIcy008Yq+97H8wuKyeb/+6LJ1l2H/b7/6Vc9QrRMvVRVL1bZWhyVwwuXwwfBlAccVX6AKQjBKJXucDiENWvWyJVmA0MxjFCYUvS7cLDPg7h8zHbtM83sux83mY32wAF9Lge8/MK1Rx9+MK98vawul9yb+srXc/fx+Y/OX11SjRkz5pfx48f/ddSoUbdGKjW5gHiIYAxCGAlLtGaX4EAAE8ykAeADfUUeNudI5SHHGSbwuMOU3VWaNGQcCKzpOQlRxY9qkwqxO5GxFGNENI1QQ8UBeaaMW0ZQUJA8ZvDgVupXXwg8S9mzmFI2D6GIaho1RDwIXHfkYSPqOHwTpHkcZ1a/+gLDEyKYwqyearo+4wDTnKqvM6emjJtN1J74+Pic9evXnxJFsdxffSFwMkw5RJ0jlqYbKg6MB2rOqG03UrkS1OtUxDmPYiMVHIJBNBvB8w9GbsCiAeHh5AGqegNEqk5wRQmMUJRSwBFGKRixMIhmNzw8GA9cnKhMV5tUiI1MhKJbz1tK4S4tY2OVrcXrJT4IBpfKyOTyE9eOJ40xjFDQIAayUKZBnNpls5ELfFqcIicugIVT1zN8CFxnT1wh6gS2pKD+h0fs1RcYouDOI6BoiUZwKCGIYFpiY5WNVLYWL8WpFK86ig9GWE0ZNxuufHkfW1KA39W0Ub/6QuDOw8BSTTjnvLJ24HD3a2Fvq5RnjLvlRqrSJYVU9asvCEYlDKMSphRhTQOxGiYOjAfuNCrvcSOVK+y+pMAhAiMVoVTTDRkHeGK5OFKZJpUF1H62PoExS2d3qKYRaqA41CypKCJwh1IQTXOINlAcSE2/pYBhnQrB46+8xqi8DXdwuTwtXp/wIYioH2JutueM0kMIDHtMKBCGgJRouGMJj8rbVGVr8fqED3tKlVKiUkUqirB/xK1+9QWYghDBkA6HEJdoNkIuLJjGVeGDUH3Aj1176GVVH0DCPVxAKVG/+sLuNkJh1NEENWgc4InlzpjyngpJlZycfFn96gtiDMWQTjGCSRRIqdZswAJwwQ0DDza4IA8boFFxRkXrVBQm6ZTCPErTiDZQHDDHVUyYMt5KSVUmx7mLnSMVhX0QXEZQmX3m12yEGA4uqXd4eKaM5wxUshF4llLKIUIpSInW7BIcSCkuDQOPGhypECYIEYowkArDqIVhX7MbHh7/0ZyqZHxC6M033/Rir74QWEmlQChC2d1ZIvXZZv3U+kdh3Ci51rfwgCeWixuVaVJZwOVXFKUZ+4dHly5dPvPb5atpV65c2+eSy2X2ma+sfRlyy9rqeFmb5Za12T4T9fH3+vysHletFdXH4szvkntd79VrGV9cvZp+wFWPuj61XZ16f/n11zMublSmPZIKlhbO2u227KioqE/Onz+/InLixM2hoaE7mjZt+kFFMnHixBjIXXny5MmV4eHhn0VERGytKI/5ZoSGfjpjxoykzZs3x8+cPPnjyMjIv8Lxq1jMJawt8G+eNu2d7c7zR0auiwgJ2anOc+WHhYUlMGG5lbXJcuH4GNYuE0+5rnxWS3X6xdqG3NilS5dumwN9mjdx4lrWRkXC+sX8ntqF9lbOmDLlc2h7eXVyIyPD9s+ZMyfus88+i5s5c+ae6aNHx7PzqGXatGkb4TptYu2zdqdOnfq3qClTtqjzXHbLli03VUYml98jqWw2mwTJkixJI1avXtEb6cVO8K3S+XfTwe/20el0DxcVWMdu3bz5RY7DHRRFaeKWVOqw8fyDDpvtjdOnT/SwS/yTCBX7Go1GsTTsVOz8imLrghD359UrVvTG2NaW6ISH1HnOZPghENKZp2hI7PLlPW0i7VxRm5CG4HgO2e3POBy2N9asWR5QyKGuleWyfLi52hRara9tT0np56lfLNdeVNQ3PT29bSG2t8rV6cysDbWMHBlgsdvps8OHDXs9JeXjv1TVbmZmJvv/Og8ZJCl469bNA6vKZZjZ7cTXas16+dixQx2glgccFovbv/tg9bC/R4axo4/NZh3E+oaQ7YF8jJux2J3K/wMAAP//+2lNHQAAAAZJREFUAwAt+NFsg8rnyAAAAABJRU5ErkJggg==",
      "name": "Area Chart with Min-Max Variance",
      "description": "",
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
    "config": "{\n  \"view\": {\n    \"stroke\": null\n  },\n  \"lineBreak\": \"[::]\",\n  \"title\": {\n    \"font\": \"Segoe UI Semibold\",\n    \"fontSize\": 18,\n    \"fontWeight\": \"normal\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#5C5347\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 11,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#8C8377\"\n  },\n  \"axis\": {\n    \"domainColor\": \"#7D7D7D\",\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12,\n    \"labelColor\": \"#605E5C\",\n    \"titleFont\": \"Segoe UI\",\n    \"titleFontSize\": 18,\n    \"titleColor\": \"#969696\",\n    \"titlePadding\": 4\n  },\n  \"axisTemporal\": {\n    \"ticks\": true,\n    \"tickDash\": [\n      2,\n      2\n    ],\n    \"tickColor\": \"#C9C9C9\",\n    \"grid\": false,\n    // \"grid\": true,\n    // \"gridColor\": \"#C9C9C9\",\n    // \"gridDash\": [\n    //   2,\n    //   2\n    // ],\n    \"domain\": true,\n    \"labelPadding\": 4\n  },\n  \"axisQuantitative\": {\n    \"ticks\": false,\n    \"grid\": false,\n    // \"grid\": true,\n    // \"gridColor\": \"#C9C9C9\",\n    // \"gridDash\": [\n    //   1,\n    //   5\n    // ],\n    \"domain\": true,\n    \"labelFlush\": false,\n    \"labelPadding\": 8\n  },\n  \"rect\": {\n    \"align\": \"center\",\n    \"baseline\": \"middle\",\n    \"strokeWidth\": 2,\n    \"cornerRadius\": 4,\n    \"stroke\": {\n      \"expr\": \"pbiColor(2)\"\n    },\n    \"fill\": {\n      \"expr\": \"pbiColor(0)\"\n    }\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#E3E3E3\"\n    },\n    \"_note_line_style\": {\n      \"strokeWidth\": 0.5,\n      \"strokeDash\": [\n        4,\n        4\n      ],\n      \"color\": \"#4A4A4A\"\n    },\n    \"_marker_label_1_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 12,\n      \"fontWeight\": \"bold\",\n      \"fontStyle\": \"italic\"\n    },\n    \"_marker_label_2_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 10,\n      \"fontWeight\": \"normal\",\n      \"fontStyle\": \"italic\"\n    },\n    \"_marker_label_3_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 10,\n      \"fontWeight\": \"bold\",\n      \"fontStyle\": \"italic\"\n    },\n    \"_note_variance_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 16,\n      \"fontWeight\": \"bold\",\n      \"fontStyle\": \"italic\"\n    },\n    \"_note_variance_%_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 12,\n      \"fontWeight\": \"normal\",\n      \"fontStyle\": \"italic\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Date",
        "description": "The temporal value for the X-axis",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__1__",
        "name": "Value",
        "description": "The quantitative value for the Y-axis",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__2__",
        "name": "Selected End Date",
        "description": "",
        "kind": "measure",
        "type": "dateTime"
      },
      {
        "key": "__3__",
        "name": "Selected Previous Months",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 10,
    "text": "Area Chart with Min-Max Variance",
    "subtitle": {
      "expr": "'Toronto Stock Exchange (TSX) Composite Index Close' + '[::]' + 'For period = ' + timeFormat( data('data_0')[0]['_min_date'], '%d-%b-%Y' ) + ' to ' + timeFormat( data('data_0')[0]['_max_date'], '%d-%b-%Y' )"
    },
    "subtitlePadding": 2
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to the dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_date"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_value"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_end_date"
    },
    {
      "calculate": "-1 * datum['__3__']",
      "as": "_months"
    },
    // calculate the start date
    {
      "calculate": "timeOffset('month', datum['_end_date'], datum['_months'])",
      "as": "_start_date"
    },
    // as records for all dates are in the dataset from Power BI, filter to only records equal to or before the selected end date and equal to or after the start date
    {
      "filter": "datum['_date'] <= datum['_end_date'] && datum['_date'] >= datum['_start_date']"
    },
    // determine the min and max Y values
    {
      "joinaggregate": [
        {
          "op": "min",
          "field": "_value",
          "as": "_min_y"
        },
        {
          "op": "max",
          "field": "_value",
          "as": "_max_y"
        }
      ]
    },
    // determine the min and max X values
    {
      "calculate": "if( datum['_value'] == datum['_min_y'], datum['_date'], toDate( null ) )",
      "as": "_min_x2"
    },
    {
      "calculate": "if( datum['_value'] == datum['_max_y'], datum['_date'], toDate( null ) )",
      "as": "_max_x2"
    },
    {
      "joinaggregate": [
        {
          "op": "max",
          "field": "_min_x2",
          "as": "_min_x"
        },
        {
          "op": "max",
          "field": "_max_x2",
          "as": "_max_x"
        }
      ]
    }
  ],
  "params": [
    {
      "name": "_area_line_colour",
      "expr": "pbiColor(5)"
    },
    {
      /*
      adjust the X and Y starting and ending coordinates as desired to configure the gradient direction
        vertical    = x1: 1, y1: 1, x2: 1, y2: 0
        horizontal  = x1: 0, y0: 0, x2: 1, y2: 1

      For more details, see https://vega.github.io/vega-lite/docs/gradient.html#linear-gradient
      */
      "name": "_area_fill_gradient_colour",
      // vertical gradient
      "expr": "{x1: 1, y1: 1, x2: 1, y2: 0, gradient: 'linear', stops: [{ offset: 0, color: 'white' }, { offset: 1, color: pbiColor(5) }]}"
      // horizontal gradient
      // "expr": "{x1: 0, y0: 0, x2: 1, y2: 1, gradient: 'linear', stops: [{ offset: 0, color: 'white' }, { offset: 1, color: pbiColor(5) }]}"
    },
    {
      "name": "_marker_label_y_space",
      "value": 14
    }
  ],
  "spacing": 8,
  "vconcat": [
    {
      "name": "DIVIDER_1",
      // adjust width as desired to suit visual
      "width": 1020,
      "height": 4,
      // hard-code a single-record dataset
      "data": {
        "values": [
          {
            "id": 1
          }
        ]
      },
      "mark": {
        "type": "rule",
        "xOffset": -70,
        "style": "_divider_rule_style"
      },
      "encoding": {
        "y": {
          "datum": 2,
          "scale": {
            "domain": [
              0,
              1
            ]
          },
          "axis": null
        },
        "x": {
          "datum": -10,
          "axis": null
        },
        "x2": {
          "datum": 0
        }
      }
    },
    {
      "name": "SLICER_SPACER",
      // adjust height as desired to suit Power BI slicers
      "width": 800,
      "height": 16,
      // hard-code a single-record dataset
      "data": {
        "values": [
          {
            "id": 1
          }
        ]
      },
      "mark": {
        "type": "bar",
        "color": "transparent"
      },
      "encoding": {
        "y": {
          "datum": 1,
          "axis": null
        },
        "x": {
          "datum": 0,
          "axis": null
        },
        "x2": {
          "datum": 1
        }
      }
    },
    {
      "name": "DIVIDER_2",
      // adjust width as desired to suit visual
      "width": 1020,
      "height": 4,
      // hard-code a single-record dataset
      "data": {
        "values": [
          {
            "id": 1
          }
        ]
      },
      "mark": {
        "type": "rule",
        "xOffset": -70,
        "style": "_divider_rule_style"
      },
      "encoding": {
        "y": {
          "datum": 2,
          "scale": {
            "domain": [
              0,
              1
            ]
          },
          "axis": null
        },
        "x": {
          "datum": -10,
          "axis": null
        },
        "x2": {
          "datum": 0
        }
      }
    },
    {
      "name": "AREA_CHART_WITH_MIN_MAX",
      "width": 960,
      "height": 440,
      "encoding": {
        "x": {
          "type": "temporal",
          "axis": {
            "title": null,
            "labelExpr": "timeFormat(datum.value, '%b %d')"
          }
        },
        "y": {
          "type": "quantitative",
          "axis": {
            "title": "Price"
          }
        }
      },
      "layer": [
        {
          "name": "LINE_AND_AREA",
          "mark": {
            "type": "area",
            "interpolate": "monotone",
            "line": {
              "color": {
                "expr": "_area_line_colour"
              },
              "strokeWidth": 4
            },
            "fill": {
              "expr": "_area_fill_gradient_colour"
            }
          },
          "encoding": {
            "x": {
              "field": "_date"
            },
            "y": {
              "field": "_value"
            }
          }
        },
        {
          "name": "MIN-MAX",
          "transform": [
            {
              "joinaggregate": [
                {
                  "op": "max",
                  "field": "__row__",
                  "as": "_max_row"
                }
              ]
            },
            // keep only a single record
            {
              "filter": "datum['__row__'] == datum['_max_row']"
            },
            // determine the variance
            {
              "calculate": "if( datum['_max_x'] > datum['_min_x'], datum['_max_y'] - datum['_min_y'], datum['_min_y'] - datum['_max_y'] )",
              "as": "_variance_y"
            },
            {
              "calculate": "datum['_variance_y'] / datum['_max_y']",
              "as": "_variance_y_%"
            },
            // determin the X coordinate for the note
            {
              "calculate": "abs( datum['_max_x'] - datum['_min_x'] ) / ( 1000 * 60 * 60 * 24 )",
              "as": "_days_x"
            },
            {
              "calculate": "if(datum['_variance_y'] >= 0, datum['_days_x'], -1 * datum['_days_x'] )",
              "as": "_days_x"
            },
            {
              "calculate": "timeOffset( 'day', datum['_min_x'], datum['_days_x'] / 2 )",
              "as": "_note_x"
            },
            // set note Y position to 120% of the max value
            {
              "calculate": "datum['_max_y'] * 1.2",
              "as": "_note_y"
            }
          ],
          "encoding": {
            "x": {
              "type": "temporal"
            },
            "y": {
              "type": "quantitative"
            }
          },
          "layer": [
            {
              "name": "NOTE_MINIMUM_VERTICAL_RULE",
              "mark": {
                "type": "rule",
                "style": "_note_line_style"
              },
              "encoding": {
                "x": {
                  "field": "_min_x"
                },
                "y": {
                  "field": "_min_y"
                },
                "y2": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_MAXIMUM_VERTICAL_RULE",
              "mark": {
                "type": "rule",
                "style": "_note_line_style"
              },
              "encoding": {
                "x": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_max_y"
                },
                "y2": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_HORIZONTAL_RULE",
              "mark": {
                "type": "rule",
                "style": "_note_line_style"
              },
              "encoding": {
                "x": {
                  "field": "_min_x"
                },
                "x2": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_MINIMUM_MARKER",
              "mark": {
                "type": "circle",
                "stroke": "white",
                // adjust the Power BI theme colour number as desired (0-based [e.g., colour 8 = (7), etc.])
                "fill": {
                  "expr": "pbiColor(7)"
                },
                // set the opacity to 1 to disable automatic transparency
                "opacity": 1,
                "size": 300
              },
              "encoding": {
                "x": {
                  "field": "_min_x"
                },
                "y": {
                  "field": "_min_y"
                }
              }
            },
            {
              "name": "NOTE_MAXIMUM_MARKER",
              "mark": {
                "type": "circle",
                "stroke": "white",
                // adjust the Power BI theme colour number as desired (0-based [e.g., colour 6 = (5), etc.])                
                "color": {
                  "expr": "pbiColor(5)"
                },
                "opacity": 1,
                "size": 300
              },
              "encoding": {
                "x": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_max_y"
                }
              }
            },
            {
              "name": "NOTE_MINIMUM_LABEL_1",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "right",
                "xOffset": -4,
                "yOffset": {
                  "expr": "10 + ( 0 * _marker_label_y_space)"
                },
                "style": "_marker_label_1_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_min_y",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "#,##0."
                },
                "x": {
                  "field": "_min_x"
                },
                "y": {
                  "field": "_min_y"
                }
              }
            },
            {
              "name": "NOTE_MINIMUM_LABEL_2",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "right",
                "xOffset": -4,
                "yOffset": {
                  "expr": "10 + ( 1 * _marker_label_y_space )"
                },
                "style": "_marker_label_2_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_min_x",
                  "type": "temporal",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "dd-MMM-yy"
                },
                "x": {
                  "field": "_min_x"
                },
                "y": {
                  "field": "_min_y"
                }
              }
            },
            {
              "name": "NOTE_MINIMUM_LABEL_3",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "right",
                "xOffset": -4,
                "yOffset": {
                  "expr": "10 + ( 2 * _marker_label_y_space )"
                },
                "lineBreak": "|",
                "style": "_marker_label_3_text_style"
              },
              "encoding": {
                "text": {
                  "value": "MIN"
                },
                "x": {
                  "field": "_min_x"
                },
                "y": {
                  "field": "_min_y"
                }
              }
            },
            {
              "name": "NOTE_MAXIMUM_LABEL_1",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "left",
                "xOffset": 4,
                "yOffset": {
                  "expr": "10 + ( 0 * _marker_label_y_space )"
                },
                "style": "_marker_label_1_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_max_y",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "#,##0."
                },
                "x": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_max_y"
                }
              }
            },
            {
              "name": "NOTE_MAXIMUM_LABEL_2",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "left",
                "xOffset": 4,
                "yOffset": {
                  "expr": "10 + ( 1 * _marker_label_y_space )"
                },
                "style": "_marker_label_2_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_max_x",
                  "type": "temporal",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "dd-MMM-yy"
                },
                "x": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_max_y"
                }
              }
            },
            {
              "name": "NOTE_MAXIMUM_LABEL_3",
              "mark": {
                "type": "text",
                "baseline": "top",
                "align": "left",
                "xOffset": 4,
                "yOffset": {
                  "expr": "10 + ( 2 * _marker_label_y_space )"
                },
                "style": "_marker_label_3_text_style"
              },
              "encoding": {
                "text": {
                  "value": "MAX"
                },
                "x": {
                  "field": "_max_x"
                },
                "y": {
                  "field": "_max_y"
                }
              }
            },
            {
              "name": "NOTE_HORIZONTAL_RECTANGLE",
              // type and position only; formatting done in "config\rect"
              "mark": {
                "type": "rect",
                "width": 100,
                "height": 40
              },
              "encoding": {
                "x": {
                  "field": "_note_x"
                },
                "y": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_VARIANCE_INDICATOR",
              "mark": {
                "type": "point",
                "shape": {
                  "expr": "datum['_variance_y'] >= 0 ? 'triangle-up' : 'triangle-down'"
                },
                "xOffset": -30,
                "yOffset": -2,
                "fontSize": 32,
                "color": {
                  "expr": "datum['_variance_y'] >= 0 ? pbiColor(5) : pbiColor(7)"
                },
                "filled": true,
                "opacity": 1,
                "size": 300
              },
              "encoding": {
                "x": {
                  "field": "_note_x"
                },
                "y": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_VARIANCE_LABEL",
              "mark": {
                "type": "text",
                "align": "left",
                "baseline": "middle",
                "xOffset": -16,
                "yOffset": -6,
                "color": "#4A4A4A",
                "style": "_note_variance_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_variance_y",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust 3-part Power BI format string as desired to suit dataset
                  "format": "+#,#.; -#,#.; 0"
                },
                "x": {
                  "field": "_note_x"
                },
                "y": {
                  "field": "_note_y"
                }
              }
            },
            {
              "name": "NOTE_VARIANCE_%_LABEL",
              "mark": {
                "type": "text",
                "align": "left",
                "baseline": "middle",
                "xOffset": -16,
                "yOffset": 10,
                "color": "#4A4A4A",
                "style": "_note_variance_%_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_variance_y_%",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust 3-part Power BI format string as desired to suit dataset
                  "format": "+#.#%; -#.#%; 0"
                },
                "x": {
                  "field": "_note_x"
                },
                "y": {
                  "field": "_note_y"
                }
              }
            }
          ]
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
- a ***title*** block with:
  - an *expression* for the subtitle with:
    - *direct data access* to retrieve the period start and end dates
    - *multi-line* presentation using a custom linebreak character string ([::])
- a standard Power BI dataset
- a ***transform*** block with:
    - 4x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - a ***calculate*** transform that uses the selected end date and period to determine the start date
    - a ***filter*** transform to restrict the dataset to those records between the period start and end dates
    - 2x ***joinaggregate*** transforms to determine the min and max X values (Date) and the min and max Y values (Price) of the filtered dataset
    - 2x ***calculate*** transforms and 2x ***joinaggregate*** transforms to determine the min and max Y values (Price) in the selected period
- a ***params*** block with:
    - 2x ***expr*** parameters to determine the area chart line and gradient colours from the Power BI theme colours as enabled by Deneb
    - a ***value*** parameter for the marker label Y (line) spacing
- a ***vconcat*** block for the 1st divider, the slicer spacer, the 2nd divider, and the area chart with min-max

>[!NOTE]
>*The example use a vertical gradient for the area chart, but simply change the X and Y settings in the area fill gradient colour expression parameter (JSON code line 96) to use a horizontal gradient*

1 - Divider 1:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

2 - Slicer Spacer:
- a transparent ***bar*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

3 - Divider 2:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

4 - Area Chart with Min-Max and Variance Note:
- a ***shared encoding*** block to ensure all layered marks use the same axis configurations
- a ***layer*** block for the area chart and the min-max points (incl. markers, labels, and variance note)

4a - Area Chart:
- an ***area*** mark with:
    - monotone ***interpolation***
    - line colour as defined in the ***params*** block above (Power BI theme colour 6)
    - gradient colour as defined in the ***params*** block above (Power BI theme colour 6 to white)

4b - Min-Max:
- a nested ***transform*** block with:
    - a ***joinaggregate/max*** to identify a single record
    - a ***filter*** transform to restrict the dataset to a single record
    - 2x ***calculate*** transforms to determine the variance and variance % Y values
    - 4x ***calculate*** transforms to determine the X and Y coordinates for the variance note
- a nested ***shared encoding*** block to ensure all layered marks use the same axis configurations
- a nested ***layer*** block for:
    - the min and max markers
    - the min and max labels
    - the vertical (min and max) and horizontal (connecting) note leader lines 
    - the note rectangle, indicator, variance, and variance %

4b (1) - Note Leader Lines:
- 3x ***rule*** marks each using a ***named style***

>[!NOTE]
>*The leader lines are first to create the desired layer order*

4b (2) - Min and Max Markers:
- 2x ***circle*** marks with:
    - ***stroke*** colour set to "white" (to give a ***halo*** effect)
    - ***fill*** colour set to a Power BI theme colour (min=8; max=6)
    - ***opacity*** set to "1" to override Vega-Lite's default transparency

4b (3) - Min Labels:
- 3x ***text*** marks with:
    - ***right*** alignment
    - ***yOffset*** values using the marker label Y (line) spacing parameter as defined in the ***params*** block above
    - a ***named style***
    - ***label formatting*** of dates and values formatted using Power BI format strings as enabled by Deneb

4b (4) - Max Labels:
- 3x ***text*** marks with:
    - ***left*** alignment
    - ***yOffset*** values using the marker label Y (line) spacing parameter as defined in the ***params*** block above
    - a ***named style***
    - ***label formatting*** of dates and values formatted using Power BI format strings as enabled by Deneb

4b (5) - Note Rectangle:
- a ***rect*** mark with:
    - ***stroke*** colour set to Power BI theme colour 3 (darker)
    - ***fill*** colour set to Power BI theme colour 1 (lighter)

4b (6) - Note Indicator:
- a ***point/shape*** mark with:
    - ***conditional shape*** (if variance >= 0 then triangle-up, else triangle-down)
    - ***conditional colour*** (if variance >= 0 then Power BI theme colour 6, else Power BI theme colour 8)
    - ***opacity*** set to "1" to override Vega-Lite's default transparency

4b (7) - Note Variance and Variance %:
- 2x ***text*** marks with:
    - ***named styles***
    - ***label formatting*** of data values via 3-part Power BI format strings as enabled by Deneb

5 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - line break character string ([::])
    - title font attributes (family, size, weight, style, colour [for each of title and subtitle])
    - general ***axis*** domain colour, label font attributes (family, size, colour), and title font attributes (family, size, colour)
    - ***X*** axis (temporal) attributes (ticks [enabled], tick dash and colour, grid [disabled], domain [enabled], label padding)
    - ***Y*** axis (quantitative) attributes (ticks [disabled], grid [disabled], domain [enabled], flush end labels [disabled], label padding)  
    - ***rect*** attributes (stroke width and colour, fill colour, corner rounding)      
    - named styles:
		- divider (colour)
        - note line (stroke width, stroke dash pattern, colour)
        - 3x marker label styles (lines 1, 2, 3)
        - 2x note label styles (variance, variance %) (font family, size, weight, style)

<hr>

As noted above, this template uses a native Power BI date picker and previous period slicer to help provide data for the Deneb/Vega-Lite visual.

The date picker uses the ***After*** style option, a disconnected date table, and a simple DAX measure to retrieve the selected value.

<img width="139" height="286" alt="212 - Image - Date Picker" src="https://github.com/user-attachments/assets/d43fec02-70cc-4349-9970-5f8277ea133f" />

``` dax
Selected End Date = MIN( 'Dates Disconnected'[Date] )
```

The table used for the previous period slicer contains period id, months, and name, and uses a simple DAX measure to retrieve the selected value:

<img width="245" height="122" alt="212 - Image - Period Table" src="https://github.com/user-attachments/assets/ed5ae715-c50b-4d40-9aac-1a128a02a772" />

``` dax
Selected Previous Months = SELECTEDVALUE( Periods[Period Months] )
```

<hr>

### Links:

Here's the template:

[912.1 - JSON - Deneb Template - Area Chart with Min-Max Variance](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/912.1%20-%20deneb_template.area_chart_with_min_max_variance.v1.8.2.json) <br>

<br>

Here's an example Power BI file using the template:

[912.2 - PBIX - Deneb Example - Area Chart with Min-Max Variance](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/912.2%20-%20Deneb%20Reusable%20Components%20-%20Area%20Chart%20with%20Min-Max%20Variance%20-%20V1.8.2.pbix) <br>

*- eof*
