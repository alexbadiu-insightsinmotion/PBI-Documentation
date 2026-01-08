<img width="1280" height="659" alt="213 - Image - Title - Waterfall Chart with Period Variance" src="https://github.com/user-attachments/assets/b21f5e27-1425-4618-aefe-6b4801ab68d9" />

## Waterfall Chart with Period Variance

*January 7, 2026*

Deneb/Vega-Lite can be used to create a waterfall chart enhanced with period variance calculations. 

This example presents a standard waterfall chart enhanced with in-period dual monthly data labels (variance and variance %), out-period columns, and an overall period variance note (complete with leader lines, note background rounded rectangle, and dual data labels (variance and variance %). Further, Power BI theme sentiment colours are used, all calculations are done in Deneb/Vega-Lite (no Power BI calculations [i.e., no DAX] are used), and Vega-Lite date picker parameters are used for the period start and end dates.

>[!NOTE]
>*The developer currently has no input into the location or appearance of the Vega-Lite parameters; adjustments are in the Deneb roadmap, and will hopefully be available in a future Deneb release*

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "070108b2-b716-4535-aead-02182298ba25",
      "generated": "2025-12-24T16:38:56.633Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJQAAABmCAYAAAAtZrjGAAAQAElEQVR4AexdCVxTx9afe5OQAGFfBGRVBEGtK6hFrfq5YIv6qqWtipZCP21fq8UFn3Wv2lbR2n7WV9dCVrAiqxuiz6qAVnApFRR3RAWRRbaQkPU7k5o+DAkiKCC5+eXP3NnOzDlzZubMHG8kg4ODjWdOH9/rw6kTXObOHcyAOA0hRCD4hP4j0H306NH0WbMmmWOEBAd6z5o1zRmXQ08/jcvPnzSJGRYWYAZpxrhMyLsT+4eGjmbhonMnTzbBIY7PDR5nMTt4nGtw8Gg2TsP1goODcbs4SuE1lgDJklebkSpiDINEAeJy2w+NFHXvzn5v4qI5702cKqUjP2cbVjBNLPUn5aQroVRa0qRSJ3GZzfTZ0ybOnvXehEl0ed2I2dPf9p81fcKKJyzlGGmtRQBTWfsPaY1Ld4JE/oo65ueYVj1DOmb29In/K61lfiKWk0yVgtaPhVgfhEyf8I8qtsqPRdSFzZkW+G7I9MAZs6dPmDzrvcB/YqV8jWVrkF0n+UnpjwWJ6bsh3MdPPMYXJh49wD9w7HsxYZ5OV8hOChLS4niJ/znB//VwHj8h/Twv/lD232UPpB+NSzp6mp9w5LwwIf0bQdKxNEH8kTQB1OHsSy7kJxzbg2nxDhxLESQeO4zjsQnHtkN9aBPi8Wm/CBLSk/nxaZn8/Uf38BLTknBdaOeg8EDaz7t3X5QZ5Ki8xkyT27bNZ/6wfqnPtrVrzfHz1g1L/fFzwIBe5gMGD1NvV7r4++67ZVab1i51wnm4PK67du1aEwAdp1EwTAmQdXVstoJAbzWQ9V83PDEJVKhQPyldHCFRKGapCFnIlg1LZ2/Z8K+lm9cvXQVYsXndvxZt+XrpYiOp6kOCRn7w/TfLVklp4o/lNaYfW9DE4eYM8XuGKUqKaywBcvny7yqWrIzaGbk6amHkmk0pkauiflmyctM6EzrJX7wiahPk8SEeBenrAd9Ert60dcmaqO8Xr9m0Y+mqjT8sXrFxvYql2EsSZNLCVZt+WrRi0z5MmIJhSoDUx/aC5d+V6cvTTo+M3CKKWPFtqXY6FX+NJdDKrpPz589nhobO6jcnOLh7SEhI//DwcM+5c+dahIcHW7eSJlXNgCVANjQ0KOVyQkyYMIfR6Sp/pVLWRyoSeclkxrbHjh3rW1JS4k6BkkFLdODmzZt25O7du2WgVHe5XEEihyPcExPDS+EIhTk8Hu/GqVOnShwdHQsNEXK5vLSysrL4ReHg4HDfEOWFee7Vq1eZ2oaKj49XwCqtAhj8V6VSMWrKyrxsrK239PRwT3gR9PDwOFpTU7Xg/v37BmsuqBXK4LWokQAePHjgzjQ3S2Iw6P+k0elBjXHn7t2gerE46GFJSdCt27eDpDJZ0N3CwiCxRKIuR6fTxpoYm2zt1s1uDSz/5o3IGsxjixVqx44d9rt27XLtykhISOjBNjFZThKEb2MNKLp/H8H2jy7/8QeKjz+AYoWx6MbNm+jx48coOTkFEYTa9fnfKiq0ACHF6K4sKw1vYBqZ/pdxhFqsUCwWq2bevHlFXRnTpk0rMmIZFTYWEH52dXFBo0ePRu8HB6N3gt5B4eFhyNfHBzGZLLRwYQQyNX1GprgKsmCZXuscsnq1Y6aAj5rhp39arFBPy3fpgCAIeU1N3c9KlSpFm1GlUolu3LiJymBVksnl6uxbt24hmexZdyPYYEgqk0bKabSH6kIG9odSKK0Bh9NKWVlZebhUJv8UsEEDuUK5wd3DY4OXd+8NtrZ2G1xc3Tb4Dx26gaTR/y4jbZCuFdWLx9TXS3Y6OTnVa5E2iCilUDqG2dnZuQK2sV2AVS8EM7OvraysTtnb29fpIGsQSZRCGcQwtx+TlEK1n6wNoiUS/HaMjz/+0CU0ONiB8uW1bMzB8DYHBBQXFweeP38+PD8/f2ZGRsbncPc0tWUUum4pUiqVmqrk5DBkajxW25fn5+dnf/fuXQeM/v37d8MhhbsOcOJbBy6ZTHBZHbW0tNwrFouFRkZG22k0WnJ9fX3AK5KRehw6G+3GegETyo7kcDhVIokM/Hi8OG1fXk5OzmMPD49HGLm5uaU4pODxiCRJkbW1NbKwsEDGxsaIzWYjT09PZGJighQKxZPOIiN3d3c24FM4JMwH3+R6uBZZLZFIvqPT6StgIjBfRj8b6wXly2vDzvPo0SNUUFCAwFWDKioq1Lfm4JHHyoX9om2g/FKrDqutrV0DvsXlsD1/Ulpa+hn0O/TevXtfgOKPfKktPSXW7kY52B7LAZzq6upfgbGDV69ePY5D2Hqjn/ap0wffh4wS/rZjXVhhGl+Ne8cEYZfjtoVdS9od9mdWKrqSkfyuLuzfv7/dXxUDuSJQKgTbM3ry5AmC7Vp9s29jYyN6FYJud4UCJkYAgx8VFha+DzeIQeAPGwd2QRDMnJmQ91p8FUrk9eDWlWG6IK6q8CNIIlAX+jsbO7QzgzWgOCVDhgzJHT9+fO7EiRNzx44dmztgwIAH0I9awEv/trtCwVJLgvIgjBs3bqhnDBi06hn0PO5gZaPFxsba7t27NxDgBg7KMdHR0S7Pq6cvH+htBKjAviiGbaG8qKio/OHDh2VgZzyCdDt99V6X9C0zRxVGzRz5b0C8FnYe3r2GCavoCl3IzUrs21oe212h4CR0CYy3lAkTJqTMmDEjZcyYMSnDhw9PAaP2YHNMwADHwYDLwUlbNnDgwKOTJ08u9Pf3Pwnxe5DX2le3TGG1RKBMjvfu3bOBVdPmzp07thB2g760liZU7SRflcqYIJCrTqiQOayirrpAQyrj1nLQ7goF9kfR5lkj7jTBzJF38jJTP8nLTN6qjfzMlChgkHB1dUUsFgsxmUwEx3PUvXt3BCcsAvJa/RWJROjatWuorq4On9AQnOAQnf5qdelFOwsTJgiQCivpQVD+02D8/wZKnwnXFVmQ3urV5EX70ZLyrVYoYCQNcAeM6yJgshi2ioc4hO0iv7mGlQgxECJMtUEQhImKUDEQAXnaIJEZ3irhngP9+eefCASKwO5COF5TU4Na+6mrqEhikYrVwwe/sXrowL6rB/j2Wu3r6bbaxoy1+ujRo5X5GamuutDa9tpQzxWM6clwgAmCVXpUcXHxaFhJ8X3Xm2BsO7WB7kuvSraBIhuY87h9+7YLDKwjMOsEg+wIjHZvA029VQsvnYtmiCsj3KxYEZ72ZhEeNiYRTmxaBE1UHpF77lC3vIyD/XVBL0HI2LngXfs9Cz901gU78skHKlK1QhdMLSzNoPpL/cLkDAEUgYL8Xl5efqm0tPQPkO8VeL4BK5MLHF4Qg8FA2N7EDVtaWqrtTlitO9M1BSJx51oDWDEIvDpUVVWpj6GYQbwdwXahag2959VJ+r/lLvGblvjqAg0pJyJS+U9dgK3RGQZqKPR1BLhHwo4fPx6RnZ09C8ef12Y759vB7bsLrPJDYVIOhMnZHxSqL9x19RKJRFUODg4xvXv3joETW8ygQYNiwI6MgdNaDPTxLqDTfMnQ0FBWeEiI54v68uqqKgTuTvbr/fr3We/r6b6+dw/X9T493dbbW7K35P6W4Hz1TIKjLrQ35zCDvwbD+3e4g8mAG+NfYGB+gO1VALM9w97Vk93e/WmuPc2dESi72qaDfqon682zaaLNs0bKMLaEjJRi4GeME/xNw/KyUnbln03d2Rg4zdm3X8/m2msuDybhuxgwId8/e/bs12BqLMTPkEZvrp56hZISCgdkyhpN13ovD/w0NtevX7fF8Pb2/vsZx3nLQp33Lpnlpo1fln7kYmJhO8HIyuE9EY09t6garXsgIlaUSY0WM8zsPrB2dC80tbE/pw22rUM2IuhsRJCspqCxWGaWbAaTxdIFJSLNmtZ5SgchppmZmdpNAidM5OzsjMDloL7sY5iw9dIk6XS9NFnmVma6+oHTSJKht57SyNway04XYKsrsLK03OXTu/euEQEBagweNEgdf3jjShmmbcQyVjKYxqq/wGLRmSwG3chE3Z4KEcaNgeVhZGqut590FltdD5fTRndP/0mgNImwYiaCF+BXc3Pz1dC/rQRB/CqTyT4FhQ/QICgoaLjmGfOFfXlgR8vPcTj8XzmcZ9/LAz9NBShSOQYU/vsZxyXiumpZg0SiDYVUUus5cNQcV2+/bUwzx7V2Tu6f2HZz/9zcxnmx54CRaz7Zwj/4+U+JHG18ti2ej1TyOqRSSppCIZHUVtVpt6WJk0hZ27TOUzoINeA7L3ySgy0EnT59GoG9h0AISFZfp5emUi7XS1NS86RW07Z2qFTK9NYjpTWVWHa68FPYONm28PGELly7cPLiwpgTH0VEH/9MAxxfFHMizM7NLU8f71JRjd5+yiV1evtJIwkRKBTC/kpYyZGjo6PaVwkrPbbj3MG0yQT5ZV68eDETtuaTcEjIBBlngi9zhnqFegXv5SlwR7y8vBAGXhXASYkvMVW4o+2JH+cF7cnkRYU9OLM/rCLnYJjs+umw0nNJYZcT/h32+O713wklkaoLpubmNYhA9dqAJb+BIBVymK31BEHUPxMiQqoiyXbn8VXIE06VCBYR9ZVKVlaW2m8JSoSbIrdu3YrwW0Bg66HDhw8j2BJRUlISgh2AplYoXOplA5ZGtdMUlj+EDXe8OmBD/mW38zx6SlmDz93cnGG6gIzYdyP3ZRzWBZ/hQXZ9hk9xZTv1H6Bkewxj2PQe4uAV4GPlPmTgP/99+HCkMGNhE8RmzLcyt7pgbGb9e2mNovJehVRS8kRWUyWmPSirU5ZIZCqj/LMpgbpAkKo23ac9Tw7a+fU11bUqFbpcVlVfcvthNbp5v9q4tFJc+aiyviJ154brW0PH7jn4zbw9uZx1H91J+OGjzJ+X7Un6OnzP/qglZ6ZPnx4zePBg3ltvvcUNCQkRjBo1ihscHMxlMpnZr0qhvoQVapSTk9MoW1vbUXAzPuqNN94YBWlTtBnrxHFvmJHT4AZ9NNgSw8CWGJGfnz+xvr5+BPRZ75vB3gFTPrR26RtNN7FZxmBZLGCwbZeQJtbrXHr2W2Pv7BEIgwjGLmoCKyc3e6D7wl+CRr9tbtntd5aJ3cXiJ3JpcaVMXCNjPAAlfiSTys4RKnRIFyaELbfy9p+0g2Q7LbNx6vGRbXeP99n2HhHuPn5fzVq5wziSf3ouRgT3Nx4GfsbwmhBSuHr16oGLFy/us2DBgr5ffvmlDw4XLVr0BpyezV6JQhEEkQfI0IUXllgLKqjkitsMI0ZWea3kAcbDClFlcUV9eZ1YeRV2p+skIs80BcqM5KerbQV9TeB/64Rv5+3s7LDtoD5xubi46Cv+dzq+QoGjPerbty/q06cP6tmzJ3JwcPg7/2U++Pq9/Y61W9/oe5XiXVLE/MKym+uXSrr5Ogf33qtnr9/jExmXeVAXzG3sJTDB0dChQ5lubm5M6CuzW7duLIe/+klrbR9fiUK1tjP66sGsbraffQKmhlu5DeHKaNbrKusZ64zMHJcZmTsu9/Eb2Xo1dwAAC5xJREFU++Mi/uncJbFnhE2RydfX3tP0KyBwAdh+Al9fXwHc/whgmRewWKx4yH8M0PsVgTunurpanY9tkbKyMvW/l1InvII/pqamCLYfhJUYdgTUq1cvBP1+bkvYLMF9q6+vR7AKq/H4cbOsPZdmswO1cuXKz8Hw+iknJ2cnSZJcOPXtAMt+J5yUfnwu5dYUUCqv1cvR1XuPReKiclHtw3Jx9aMnktLSKkmJnEG7SSDiN12AvqnwKgLOYvTmm28ib29vtVBh8FvTC3UdWF25gNk68D6k1asL6f6zGQZ4JPgZR8LpaCTcfY2EVWokXFWMdOjRN9t7yIRyS5f+impk46AwcTFjdfMlmXbe9LBNwji5jFipC18Jzt3S3dRfqVhp4WZdrRBgp2Jnd5MXUP8q+czfwzBhwuHAFA4Hp/AePXqEw2VpOPQzHEo166iHfL3fZhWqsLDwg2+//faLkpKSeeCre3/z5s2fnjlzZh64Aj7QS7ENGb38Ji126jn4R0t7ty9tHHoutnXuFWlu77HKyrHXyq84p05Fxmbs0wXcJF4RsPGPVwd8vIX+qv9BGc5rT2BlA2TqAvRjfINMsbys4slntbV1U0pKH88oLLz3iQqRYZA3eHl8RpkuQJ7eL7TzC0wof7BX/UFx/T09Pf1hJfWHyeQPeUf0VYQ8fEKNhlAXmjUF9NHE6c0qlI+Pj3znzp0ILq/QV199hfh8PoqIiEBjx45tgLsPJSagDQKpWu1bglOCHGa22u7Atgrs6Qjv6SAo7Wa045stLCymgL0zBWbaFJhxU/z8/KZA/SkgsBYIR5vcq4tjuwwDFABBf5GlpSXCvLalReAxRxfaQrO1dfUqFNy3mBw6dKgIrPc8UKI8sOSvgkWfhxEXF1cQ+VPq7nqvzM+0ERmbuay1ncH18Eqj2c/xUg7OUbzSEDhPH0CY+BBwEMIm0Feng9KrYTURwZZc0K9fvwKYsAWwmhSwWKz70B8p4LX/6lUozNnly5crbt261YBx+/ZtMQ4xwJaqR9bWqrVrkVIbuF4bsAZWmkDYxwNhVQqEmRsI+3ogrDTYFdAGsp2jKij8DgAb4KMFV4jndo5etq0XaoWaM2eOjbZzmMfbadU20i9eG4T6J+CYDqS/ODWqRkdIgMTKhJB8hMqEGdDYOXzrVrEtnAKM4TqdrgNGcLy0g9XKnsItg5IBbNk2OvSBjj9gA1uQPB6vQiyWHeJyn/3R1nXr1t2EewoxHEPlOiCF43AZnCgeU/A0KBmAXVuhQx/g4C+XNzQ0VKu3vHjqR1s7Ynfokm2qFaoLcUax0sESoBSqgwegqzVPKVRXG9EO5odSqA4egK7WPKVQXW1EO5gfSqE6eAC6WvOUQnW1Ee1gfjqtQnWwXKjmWykB9X/ACO4Xr87gy2slD1S1TiQB/FtNKpVK5oi0XvR86sszBR+NkTawj6+urs65uLjYlYJhycDIyMgR/HlNdALriNqXB24XqUQiz+Rwnn3R86kvTwROGqk2sI+PzWY/cHJyKqJgWDKQSqUl4M9rohNYRyhfXifaKrpKVyijvKuMZCfhg1KoTjIQXaUbr16huoqkKD5aJAFKoVokJqpQSyVAKVRLJUWVa5EEKIVqkZioQi2VAKVQLZUUVa5FEqAUqkViogq1VAJqX97s2bN9QqZNcwwJCekfHh7uOXfuXIuOeC+vpZ2mynVeCWBfHgnOPCuSbdzkvTzw25iAj4bxF+iNQ1Z5ebljUVGREwXDkgH46+zAl9dYF9TP4N9lQJ4FCb48MfhgzvN4wgROox9txb488NvUg49GpgMSW1vbEldX12IKhiUD0JUy8OU10Qnw78ogj3ovr/NuHq9nzyij/PUct07ba0qhOu3QvJ4doxTq9Ry3TttrSqE67dC8Ph1r3FNKoRpLg3puswQohWqzCCkCjSVAKVRjaVDPbZYApVBtFiFFoLEEyODgYNrcGTNsqffyGouFem6tBLDrRSEiSXvqNzYN67cyW/vbqODHa/43NrEmgs/uOvUbm4b1W5k6fxvV8/kyAD8e9RubeNJQaB8JUEZ5+8jZYFqhFMpghrp9GKUUqn3kbDCtUAplMEPdPoxSCtU+cjaYViiF6pJD3XFMUQrVcbLvki1TCtUlh7XjmKIUquNk3yVb1lYoIjQ01F3zoqepqamRq6srUxuQzuiS0qCYeq4EmEwmy9bWlqGtE46OjkagF8bPKBQok4VKJfOSikRep0/nsIcNG7ZjwIB+3/oNGrR+8OABGwICAlaNHjHiq6FDh25OTU11SkxM9Nq+ffsgDPzcGLGxsX2ioqICoqK+fatxuuZ5z549b+AymnjjUJOniy6mqa/epm++GbNjx46BjWlpnjdu3Dhi06Zv/mffvn0++/fv99ak4xBojtz+449D8bM2cB1cVzsdxzX9xM/a+H7jxje3bds2TB8P0GYArq9dD6f9qKcvuA4GLqOrnj654LK4H7iedhmcpq89DQ+4vgaPHj0Sz5kzJ+ytgIAVQ4YMWTds0KD1bw4duiYMPgwGo+gZheJwOFVcrjCdIxTmREdHXwf88XtWFj0rKwtlZp4rOX78uDwtLY3+K59fOnXq1OvTpk27cfH8ebML2eeGHTxwwCcuLu42TsM4ceJEUX7+n5bXrl3tl5qcPORQYiKB0zXIyMhA/0lP9z2YnOyVkJDwSJOOw3PnfqtLP3LEJTs72xrHNQD696/l5ToeO3KkJ9Tz16Z57WZeSfbvZ0cnJyeMA4V/rKmHw4KCK9VXr15FaWkp3kePHq3EaRpcvZorybl8of+hpKSR2jQLrlx7cu1anktycvJwgEhTB4fqfqal9U9NOvCmNg9XCnIrL2Znv5Fz/vxAbZr5+X/Qrl654pJx6tSI1NQEJqalQWZmpuLy5QvOSUkHBmnnPa3X41zWqbEHk5KcNXVwqO4LyCw1Kak/8C7FaRqA3G5fys7ulnXmjCceF006DnF7ubmXeqckJvqlJia64TQN8m/8UXjhwnnPg4mJAZq8sWPH5vr5+WWnp6fXZWT8Vn0y84z5qZMni0DRrwwfPvzSMwqlvd6BQtVy+LH8aC53P5fLPcPj8Q5xBILkaIHgOi47f/58poIgxISKvEiQZKEFnW6L0zFwXS5XcDgmRrAdkeQRJZ1+D6drALT+/IXDiY8BmkKhsEaTjsPo6Ng70E4alDmB4xrgt5xjeMIDXIEglaZQnAKapZo8HHI4cQUMpvF2sVgaw4HJgdM04HCEV7hc4X+gTHJMTEyZJh2HkJfD5Qp2R/P5v2h4w+kYMQLBJciLg75wAQ9xGgb+d2Q0BcOYwWTmypRENnjhjXC6BtBOAfRzN1cHTS439gyHz9/HEwp/hravaOrgEOScz2SapEokshQOR6iVp67HVyLGThWNdgmX10AjM6AbD7wXatJxCHJTRPN4RyEvEY8LTtMAtxcTw+MyFYpjcoTyNOk4jI7eV8zjCQV1DQ37jExMTuE0DWL4/JNcWHx4PMFekNsFaEOM85pVKFygOcDyh+t7KpRKJxUDmcqMCGek4wMMVgEkOrJanbRXKHwANKu0CezevVumYU4772XGraysyAaV3FUqFvckCMKLwSACXhb95/HA4XAkgKqX1R6mszsurlwgEJTgZ21geeI+aafrimOF0JXeojTcEMzaWJ5QmAQr0VmYeRdbVLELFMIC5vGER2EVSoWBSObxYlO6AFttZqFNCtXm1ikCXU4CBqtQkyZN+uKdd97pCxg8efJkE19fXyOwi4wnTJhgHxgY6D1u3DgL7dHePHPk1KiZI4Khrrl2niZ+JTP5g7yM5MlAt8fEiRMdNemGEhqsQpEk+alSqeyjUCiwDEJ79OjxpUgk8oaBtwe8C/ctM0FxFgcFBX3x9ttvz5syZYoZItBoQoXGq1Qqb1C6EFDE2ZC3Hsp8DGEkLkMiYjxBEm+BXWVJp9PnQN4syPscFOwzoLcKwomoC3/+HwAA//9bqakdAAAABklEQVQDAJK0pwsV6OcrAAAAAElFTkSuQmCC",
      "name": "Waterfall Chart with Period Variance",
      "description": "A standard waterfall chart enhanced with dual monthly data labels (variance and variance %), an overall period variance note with leader lines, note background rounded rectangle, dual data labels (variance and variance %) Power BI theme sentiment colours are used.",
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
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"lineBreak\": \"|\",\r\n  \"title\": {\r\n    \"font\": \"Segoe UI Semibold\",\r\n    \"fontSize\": 18,\r\n    \"fontWeight\": \"normal\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#5C5347\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 14,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#8C8377\"\r\n  },\r\n  \"axis\": {\r\n    \"domain\": true,\r\n    \"domainColor\": \"#7D7D7D\",\r\n    \"ticks\": false,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14,\r\n    \"labelColor\": \"#605E5C\"\r\n  },\r\n  \"axisDiscrete\": {\r\n    \"grid\": false,\r\n    \"labelAngle\": 0,\r\n    \"labelAlign\": \"center\",\r\n    \"labelPadding\": 4\r\n  },\r\n  \"axisQuantitative\": {\r\n    \"grid\": true,\r\n    \"gridColor\": \"#E3E3E3\",\r\n    \"labelPadding\": 4\r\n  },\r\n  \"legend\": {\r\n    \"title\": null,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"style\": {\r\n    \"_note_vertical_leader_rule_style\": {\r\n      \"strokeDash\": [\r\n        2,\r\n        2\r\n      ],\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_note_horizontal_leader_rule_style\": {\r\n      \"strokeWidth\": 1.5,\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_note_rect_style\": {\r\n      \"cornerRadius\": 20,\r\n      \"stroke\": \"#E3E3E3\",\r\n      \"color\": \"#FBFAF9\"\r\n    },\r\n    \"_note_variance_label_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 18,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#000000\"\r\n    },\r\n    \"_note_variance_percent_label_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_out_period_bar_style\": {\r\n      \"cornerRadiusEnd\": 4,\r\n      \"stroke\": \"#FFFFFF\",\r\n      \"color\": \"#4A4A4A\",\r\n      \"opacity\": 0.8\r\n    },\r\n    \"_out_period_value_background_rect_style\": {\r\n      \"cornerRadius\": 4,\r\n      \"color\": \"#FFFFFF\"\r\n    },\r\n    \"_out_period_value_text_style\": {\r\n      \"font\": \"Segoe UI\",      \r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#000000\"\r\n    },\r\n    \"_in_period_bar_style\": {\r\n      \"cornerRadius\": 4,\r\n      \"opacity\": 0.6\r\n    },\r\n    \"_in_period_variance_background_rect_style\": {\r\n      \"cornerRadius\": 4,\r\n      \"color\": \"#FFFFFF\"\r\n    },\r\n    \"_in_period_variance_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_in_period_variance_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Date",
        "description": "The temporal dataset value (e.g., Date); will be aggregated into months before being displayed on the X axis",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__1__",
        "name": "Value",
        "description": "The quantitative dataset value (e.g., Total Sales) to be displayed on the Y axis",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    // adjust the space between the title/subtitle and the visual as desired
    "offset": 20,
    "text": "Waterfall Chart with Period Variance",
    "subtitle": "Net Performance Analysis",
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
    // calculate the current year and month
    {
      "calculate": "year( datum['_date'] )",
      "as": "_current_year"
    },
    {
      "calculate": "month( datum['_date'] )",
      "as": "_current_month"
    },
    // aggregate the dataset into months
    {
      "aggregate": [
        {
          "op": "sum",
          "field": "_value",
          "as": "_current_month_value"
        }
      ],
      "groupby": [
        "_current_year",
        "_current_month"
      ]
    },
    // get the previous month value
    {
      "window": [
        {
          "op": "lag",
          "field": "_current_month_value",
          "as": "_previous_month_value"
        }
      ],
      "frame": [
        null,
        0
      ],
      "sort": [
        {
          "field": "_current_year",
          "order": "ascending"
        },
        {
          "field": "_current_month",
          "order": "ascending"
        }
      ]
    },
    {
      "calculate": "datum['_current_year'] + ( pad( datum['_current_month'] + 1, 2, '0', 'left' ) )",
      "as": "_current_year_month"
    },
    {
      "window": [
        {
          "op": "rank",
          "as": "_year_month_rank"
        }
      ],
      "sort": [
        {
          "field": "_current_year_month",
          "order": "ascending"
        }
      ]
    },
    // get the in-period min and max rank
    {
      "calculate": "datum['_current_year_month'] == _in_period_start_year_month ? datum['_year_month_rank'] : null",
      "as": "_in_period_min_rank"
    },
    {
      "calculate": "datum['_current_year_month'] == _in_period_end_year_month ? datum['_year_month_rank'] : null",
      "as": "_in_period_max_rank"
    },
    {
      "joinaggregate": [
        {
          "op": "max",
          "field": "_in_period_min_rank",
          "as": "_in_period_min_rank2"
        },
        {
          "op": "max",
          "field": "_in_period_max_rank",
          "as": "_in_period_max_rank2"
        }
      ]
    },
    // filter to keep only the in-period and out-period records
    {
      "filter": "datum['_year_month_rank'] >= ( datum['_in_period_min_rank2'] - 1 )"
    },
    {
      "filter": "datum['_year_month_rank'] <= ( datum['_in_period_max_rank2'] + 1 )"
    },
    // compose a composite x-axis label
    {
      "calculate": "datum['_current_year_month'] == _out_period_start_year_month ? '000-00-BEGIN' : datum['_current_year_month'] == _out_period_end_year_month ? '999-99-END' : ( datum['_year_month_rank'] + 100 ) + '-' + pad( datum['_current_month'] + 1, 2, '0', 'left' ) + '-' + monthAbbrevFormat( datum['_current_month'] ) + '|' + datum['_current_year']",
      "as": "_x_axis_label"
    }
  ],
  "params": [
    // get the user-selected start and end dates
    {
      "name": "_string_start_date",
      "value": "2023-04-01",
      "bind": {
        "input": "date",
        "name": "Start Date:‎ ‎"
      }
    },
    {
      "name": "_string_end_date",
      "value": "2024-09-30",
      "bind": {
        "input": "date",
        "name": "End Date:‎ ‎ "
      }
    },
    // get the selected date components
    {
      "name": "_in_period_start_year",
      "expr": "toNumber( slice( _string_start_date, 0, 4 ) )"
    },
    {
      "name": "_in_period_start_month",
      "expr": "toNumber( slice( _string_start_date, 5, 7 ) )"
    },
    {
      "name": "_in_period_end_year",
      "expr": "toNumber( slice( _string_end_date, 0, 4 ) )"
    },
    {
      "name": "_in_period_end_month",
      "expr": "toNumber( slice( _string_end_date, 5, 7 ) )"
    },
    // calculate the in-period start date and end date
    {
      "name": "_in_period_start_date",
      "expr": "datetime( _in_period_start_year, _in_period_start_month - 1, 1 )"
    },
    {
      "name": "_interim_in_period_end_date1",
      "expr": "datetime( _in_period_end_year, _in_period_end_month - 1)"
    },
    {
      "name": "_interim_in_period_end_date2",
      "expr": "timeOffset( 'month', _interim_in_period_end_date1, 1)"
    },
    {
      "name": "_in_period_end_date",
      "expr": "timeOffset( 'day', _interim_in_period_end_date2, -1)"
    },
    // calculate the out-period start date and end date
    {
      "name": "_out_period_start_date",
      "expr": "timeOffset( 'month', _in_period_start_date, -1)"
    },
    {
      "name": "_out_period_end_date",
      "expr": "timeOffset( 'month', _in_period_end_date, 1)"
    },
    // calculate the in-period and out-period year_month (for use in subsequent filters)
    {
      "name": "_in_period_start_year_month",
      "expr": "(_in_period_start_year * 100 ) + _in_period_start_month"
    },
    {
      "name": "_in_period_end_year_month",
      "expr": "(_in_period_end_year * 100 ) + _in_period_end_month"
    },
    {
      "name": "_out_period_start_year_month",
      "expr": "( year( _out_period_start_date ) * 100 ) + ( month(  _out_period_start_date ) + 1 )"
    },
    {
      "name": "_out_period_end_year_month",
      "expr": "( year( _out_period_end_date ) * 100 ) + ( month(  _out_period_end_date ) + 1 )"
    }
  ],
  "vconcat": [
    {
      "name": "WATERFALL_CHART",
      "width": 1100,
      "height": 670,
      // shared encoding for all layered marks
      "encoding": {
        // formatting done in "config/axis" and "config/axisDiscrete"
        "x": {
          "field": "_x_axis_label",
          "type": "ordinal",
          "axis": {
            "title": null,
            // display only from character 7 onwards (only include year if 1st record or January [rank 101 or month = 01])
            "labelExpr": "slice( datum.value, 0, 3 ) == '000' || slice( datum.value, 0, 3 ) == '999' ? slice( datum.value, 7, 100 ) : slice( datum.value, 0, 3 ) == '101' || slice( datum.value, 4, 6 ) == '01' ? slice( datum.value, 7, 100 ) : slice( datum.value, 7, 10 )"
          }
        },
        // formatting done in "config/axis" and "config/axisQuantitative"
        "y": {
          "type": "quantitative",
          "axis": {
            "title": null,
            "tickCount": 7,
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,##0,. K"
          }
        }
      },
      "layer": [
        {
          "name": "NOTE",
          "transform": [
            // calculate the Y value for the out-period records
            {
              "calculate": "datum['_x_axis_label'] == '000-00-BEGIN' ? datum['_current_month_value'] : datum['_x_axis_label'] == '999-99-END' ? datum['_previous_month_value'] : datum['_current_month_value']",
              "as": "_out_period_y_value"
            },
            {
              "joinaggregate": [
                {
                  "op": "max",
                  "field": "_current_month_value",
                  "as": "_max_y_value"
                }
              ]
            },
            // filter to keep only the out-period records
            {
              "filter": "datum['_year_month_rank'] == ( datum['_in_period_min_rank2'] - 1 ) || datum['_year_month_rank'] == ( datum['_in_period_max_rank2'] + 1 )"
            },
            // adjust multiplier to suit dataset
            {
              "calculate": "datum['_max_y_value'] * 1.15",
              "as": "_out_period_note_y_value"
            },
            // calculate the out-period variance and variance %
            {
              "calculate": "datum['_x_axis_label'] == '000-00-BEGIN' ?datum['_current_month_value'] : null",
              "as": "_out_period_begin_value1"
            },
            {
              "calculate": "datum['_x_axis_label'] == '999-99-END' ? datum['_previous_month_value'] : null",
              "as": "_out_period_end_value1"
            },
            {
              "joinaggregate": [
                {
                  "op": "max",
                  "field": "_out_period_begin_value1",
                  "as": "_out_period_begin_value2"
                },
                {
                  "op": "max",
                  "field": "_out_period_end_value1",
                  "as": "_out_period_end_value2"
                }
              ]
            },
            {
              "calculate": "datum['_out_period_end_value2'] - datum ['_out_period_begin_value2']",
              "as": "_out_period_variance"
            },
            {
              "calculate": "datum['_out_period_variance'] / datum ['_out_period_begin_value2']",
              "as": "_out_period_variance_percent"
            }
          ],
          "layer": [
            {
              "name": "NOTE_VERTICAL_LEADER_LINES",
              "mark": {
                "type": "rule",
                "style": "_note_vertical_leader_rule_style"
              },
              "encoding": {
                "x": {
                  "field": "_x_axis_label"
                },
                "y": {
                  "field": "_out_period_y_value"
                },
                "y2": {
                  "field": "_out_period_note_y_value"
                }
              }
            },
            {
              "name": "NOTE_HORIZONTAL_LEADER_LINE",
              // only keep a single record
              "transform": [
                {
                  "filter": "datum['_year_month_rank'] == (datum['_in_period_max_rank2'] + 1 )"
                }
              ],
              "mark": {
                "type": "rule",
                "style": "_note_horizontal_leader_rule_style"
              },
              "encoding": {
                "x": {
                  "datum": "000-00-BEGIN"
                },
                "x2": {
                  "datum": "999-99-END"
                },
                "y": {
                  "field": "_out_period_note_y_value"
                }
              }
            },
            {
              "name": "NOTE_RECTANGLE",
              // only keep a single record
              "transform": [
                {
                  "filter": "datum['_year_month_rank'] == (datum['_in_period_max_rank2'] + 1 )"
                }
              ],
              "mark": {
                "type": "rect",
                "width": 140,
                "height": 40,
                "style": "_note_rect_style"
              },
              "encoding": {
                "x": {
                  "value": {
                    "expr": "width/2"
                  }
                },
                "y": {
                  "field": "_out_period_note_y_value"
                }
              }
            },
            {
              "name": "NOTE_VARIANCE_LABEL",
              // only keep a single record
              "transform": [
                {
                  "filter": "datum['_year_month_rank'] == (datum['_in_period_max_rank2'] + 1 )"
                }
              ],
              "mark": {
                "type": "text",
                "align": "center",
                "baseline": "bottom",
                "yOffset": 4,
                "style": "_note_variance_label_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_out_period_variance",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI 3-part format string as desired to suit dataset
                  "format": "+#,. K; -#,. K; 0"
                },
                "x": {
                  "value": {
                    "expr": "width/2"
                  }
                },
                "y": {
                  "field": "_out_period_note_y_value"
                }
              }
            },
            {
              "name": "NOTE_VARIANCE_PERCENT_LABEL",
              // only keep a single record
              "transform": [
                {
                  "filter": "datum['_year_month_rank'] == (datum['_in_period_max_rank2'] + 1 )"
                }
              ],
              "mark": {
                "type": "text",
                "align": "center",
                "baseline": "top",
                "yOffset": 4,
                "style": "_note_variance_percent_label_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_out_period_variance_percent",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI 3-part format string as desired to suit dataset
                  "format": "+#.#%; -#.#%; 0"
                },
                "x": {
                  "value": {
                    "expr": "width/2"
                  }
                },
                "y": {
                  "field": "_out_period_note_y_value"
                }
              }
            }
          ]
        },
        {
          "name": "OUT_PERIOD",
          "transform": [
            {
              "filter": "datum['_current_year_month'] == _out_period_start_year_month || datum['_current_year_month'] == _out_period_end_year_month"
            },
            {
              "calculate": "datum['_x_axis_label'] == '000-00-BEGIN' ? datum['_current_month_value'] : datum['_x_axis_label'] == '999-99-END' ? datum['_previous_month_value'] : null",
              "as": "_out_period_y_value"
            }
          ],
          "layer": [
            {
              "name": "OUT_PERIOD_COLUMN",
              "mark": {
                "type": "bar",
                "width": {
                  "band": 0.95
                },
                "style": "_out_period_bar_style"
              },
              "encoding": {
                "y": {
                  "field": "_out_period_y_value"
                }
              }
            },
            {
              "name": "OUT_PERIOD_COLUMN_BACKGROUND_RECTANGLES",
              "mark": {
                "type": "rect",
                "width": {
                  "band": 0.95
                },
                "height": 20,
                "align": "center",
                "baseline": "bottom",
                "yOffset": 0,
                "style": "_out_period_value_background_rect_style"
              },
              "encoding": {
                "y": {
                  "field": "_out_period_y_value"
                }
              }
            },
            {
              "name": "OUT_PERIOD_VALUES",
              "mark": {
                "type": "text",
                "align": "center",
                "baseline": "bottom",
                "yOffset": -2,
                "style": "_out_period_value_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_out_period_y_value",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "#,##0,. K"
                },
                "y": {
                  "field": "_out_period_y_value"
                }
              }
            }
          ]
        },
        {
          "name": "IN_PERIOD",
          "transform": [
            {
              "filter": "datum['_current_year_month'] >= _in_period_start_year_month"
            },
            {
              "filter": "datum['_current_year_month'] <= _in_period_end_year_month"
            },
            // redo the ranking to account for the in-period date filters
            {
              "window": [
                {
                  "op": "rank",
                  "as": "_year_month_rank"
                }
              ],
              "sort": [
                {
                  "field": "_current_year_month",
                  "order": "ascending"
                }
              ]
            },
            // redo the composite x-axis label to account for the updated ranking
            {
              "calculate": "datum['_current_year_month'] == _out_period_start_year_month ? '000-00-BEGIN' : datum['_current_year_month'] == _out_period_end_year_month ? '999-99-END' : ( datum['_year_month_rank'] + 100 ) + '-' + pad( datum['_current_month'] + 1, 2, '0', 'left' ) + '-' + monthAbbrevFormat( datum['_current_month'] ) + '|' + datum['_current_year']",
              "as": "_x_axis_label"
            },
            // calculate the in-period variance and variance %
            {
              "calculate": "datum['_current_month_value'] - datum ['_previous_month_value']",
              "as": "_in_period_value_variance"
            },
            {
              "calculate": "datum['_in_period_value_variance'] / datum ['_previous_month_value']",
              "as": "_in_period_value_variance_percent"
            },
            {
              "calculate": "datum['_in_period_value_variance'] < 0 ? datum['_current_month_value'] : datum['_previous_month_value']",
              "as": "_in_period_value_minimum"
            },
            {
              "calculate": "datum['_in_period_value_variance'] >= 0 ? datum['_current_month_value'] : datum['_previous_month_value']",
              "as": "_in_period_value_maximum"
            },
            {
              "calculate": "datum['_in_period_value_variance'] >= 0 ? datum['_in_period_value_maximum'] : datum['_in_period_value_minimum']",
              "as": "_in_period_y_value"
            }
          ],
          "layer": [
            {
              "name": "IN_PERIOD_COLUMN",
              "mark": {
                "type": "bar",
                "width": {
                  "band": 0.95
                },
                "color": {
                  "expr": "datum['_in_period_value_variance'] >= 0 ? pbiColor('positive') : pbiColor('negative')"
                },
                "style": "_in_period_bar_style"
              },
              "encoding": {
                "y": {
                  "field": "_previous_month_value"
                },
                "y2": {
                  "field": "_current_month_value"
                }
              }
            },
            {
              "name": "IN_PERIOD_VARIANCE_BACKGROUND_RECTANGLES",
              "mark": {
                "type": "rect",
                // "width": 60,
                "width": {
                  "band": 0.95
                },
                "height": 26,
                "align": "center",
                "yOffset": {
                  "expr": "datum['_in_period_value_variance'] >= 0 ? -16 : 16 "
                },
                "style": "_in_period_variance_background_rect_style"
              },
              "encoding": {
                "y": {
                  "field": "_in_period_y_value"
                }
              }
            },
            {
              "name": "IN_PERIOD_VARIANCE_LABEL",
              "mark": {
                "type": "text",
                "align": "center",
                "yOffset": {
                  "expr": "datum['_in_period_value_variance'] >= 0 ? -10 : 10"
                },
                "style": "_in_period_variance_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_in_period_value_variance",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI 3-part format string as desired to suit dataset
                  "format": "+#,. K; -#,. K; 0"
                },
                "y": {
                  "field": "_in_period_y_value"
                }
              }
            },
            {
              "name": "IN_PERIOD_VARIANCE_PERCENT_LABEL",
              "mark": {
                "type": "text",
                "align": "center",
                "yOffset": {
                  "expr": "datum['_in_period_value_variance'] >= 0 ? -22 : 22"
                },
                "style": "_in_period_variance_percent_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_in_period_value_variance_percent",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI 3-part format string as desired to suit dataset
                  "format": "+#.#%; -#.#%; 0"
                },
                "y": {
                  "field": "_in_period_y_value"
                }
              }
            }
          ]
        }
      ]
    },
    {
      "name": "LEGEND",
      "width": 1100,
      "height": 1,
      "data": {
        "values": [
          {
            "legend_id": 1,
            "legend_size": 1,
            "legend_label": "Total / Balance"
          },
          {
            "legend_id": 2,
            "legend_size": 1,
            "legend_label": "Increase"
          },
          {
            "legend_id": 3,
            "legend_size": 1,
            "legend_label": "Decrease"
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
              "Total / Balance",
              "Increase",
              "Decrease"
            ],
            "range": [
              "#4A4A4A",
              {
                "expr": "pbiColor('positive')"
              },
              {
                "expr": "pbiColor('negative')"
              }
            ]
          },
          "legend": {
            // position only; formatting done in "config\legend"
            "direction": "horizontal",
            "orient": "none",
            // adjust X and Y legend position as desired to suit visual
            // ref: https://vega.github.io/vega-lite/docs/legend.html#properties
            "legendX": {
              "expr": "(width / 2 ) - 120"
            },
            "legendY": 720
          }
        }
      }
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
- a ***transform*** block with:
    - 2x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - 2x ***calculate*** transforms to extract the year and month from the Power BI date field
    - an ***aggregate*** transform to aggregate the dataset values into months
    - a ***window/lag*** transform to get the previous month's value
    - a ***calculate*** transform that uses the extracted year and month to create a composite year-month
    - a ***window/rank*** transform to rank the composite year-month
    - 2x ***calculate*** transforms and 2x ***joinaggregate*** transforms to determine the min and max ranks in the selected period
    - 2x ***filter*** transforms to restrict the dataset to those records between the selected start and end dates and 1 month outside the period
    - a ***calculate*** transform to compose a composite X-axis label 
- a ***params*** block with:
    - 2x ***date*** screen widget parameters to allow the user to select the period of interest
    - 4x ***expr*** parameters to extract the year and month from the selected start and end date strings
    - 4x ***expr*** parameters to calculate in-period start and end dates (first day of the month containing the selected start date and last day of the month containing the selected end date)
    - 2x ***expr*** parameters to calculate out-period start and end dates
    - 4x ***expr*** parameters to calculate the in-period and out-period start and end composite year-month
- a ***vconcat*** block for the waterfall chart and the custom legend

1 - Waterfall Chart:
- a ***shared encoding*** block to ensure all layered marks use the same axis configurations
 	- a custom ***labelExpr*** expression is used for the ***X-axis*** labels to extract the out-period descriptiors (BEGIN; END) and the in-period month and year (year extracted for the 1st record and for each January record only)
    - ***label formatting*** of ***Y-axis*** values formatted using Power BI format strings as enabled by Deneb
- a ***layer*** block for the variance note, the out-period columns (absolute value), and the in-period variance columns

1a - Variance Note:
- a nested ***transform*** block with:
	- a ***calculate*** transform to select the appropriate value for the out-period records (current month value for the "BEGIN" record and previous month value for the "END" record)
	- a ***joinaggregate*** transform to determine the max in-period Y value (so note can be positioned above max value and not overlap)
    - a ***filter*** transform to restrict the dataset to only the out-period records
    - a ***calculate*** transform to determine the note Y position (15% above the max in-period value)
    - 2x ***calculate*** transforms and 2x ***joinaggregate*** transforms to determine the out-period ***Y*** values
    - 2x ***calculate*** transforms to determine the out-period variance and variance %

1a (1) - Note Vertical Leader Lines:
- a ***rule*** mark with:
	- a ***dotted*** line
 	- a constant ***X*** value and ***ranged Y*** values to make the line vertical-only
  	- a ***named style***- 

1a (2) - Note Horizontal Leader Line:
- a nested ***transform*** block with:
	- a ***filter*** transform to restrict the dataset to only a single record
- a ***rule*** mark with:
	- a ***solid*** line
 	- ***ranged X*** values and a constant ***Y*** value (the note ***Y*** position calculated above) to make the line horizontal-only
  	- a ***named style***- 

1a (3) - Note Background Rectangle:
- a nested ***transform*** block with:
	- a ***filter*** transform to restrict the dataset to only a single record
- a ***rect*** mark with:
	- ***rounded corners***
 	- an ***X*** position 1/2 the visual width
	- a ***named style***

1a (4) - Note Variance Label:
- a nested ***transform*** block with:
	- a ***filter*** transform to restrict the dataset to only a single record
- a ***text*** mark with:
	- ***label formatting*** using a 3-part Power BI format string as enabled by Deneb to display signed values
 	- an ***X*** position 1/2 the visual width
	- a ***named style***

1a (5) - Note Variance % Label:
- a nested ***transform*** block with:
	- a ***filter*** transform to restrict the dataset to only a single record
- a ***text*** mark with:
	- ***label formatting*** using a 3-part Power BI format string as enabled by Deneb to display signed values
 	- an ***X*** position 1/2 the visual width
	- a ***named style***

1b - Out-Period:
- a nested ***transform*** block with:
	- a ***filter*** transform to restrict the dataset to only the 2 out-period records
 	- a ***calculate*** transform to assign the appropriate Y value to both records
- a ***layer*** block for the out-period column, the out-period value background rectangles (same colour as visual background to maintain label clarity), and the out-period value

1b (1) - Out-Period Column:
- a ***bar*** mark with:
	- exchanged ***X and Y encoding*** so the bar is rendered as a column
	- 95% ***band width***
 	- a ***named style*** 

1b (2) - Out-Period Value Background Rectangle:
- a ***rect*** mark with:
	- ***rounded corners***
 	- 95% ***band width***
	- same colour as the visual background (white) to ensure clarity when label overlaps Y-axis gridlines
	- a ***named style***

1b (3) - Out-Period Value Label:
- a ***text*** mark with:
	- ***label formatting*** using a Power BI format string as enabled by Deneb
	- a ***named style***

1c - In-Period:
- a nested ***transform*** block with:
	- 2x ***filter*** transforms to restrict the dataset to only in-period records
    - a ***window/rank*** transform to redo the ranking of the composite year-month (now with only in-period records)
    - a ***calculate*** transform to redo the composite X-axis label (now with only in-period records)
    - 2x ***calculate*** transforms to determine the in-period month-to-month variance and variance %
    - 3x ***calculate*** transforms to determine the in-period min, max, and Y position (for the background rectangles, variance, and variance % labels)
- a ***layer*** block for the in-period column, the in-period value background rectangles (same colour as visual background to maintain label clarity), the in-period variance, and the in-period variance %

1c (1) - In-Period Column:
- a ***bar*** mark with:
	- exchanged ***X and Y encoding*** so the bar is rendered as a column
	- 95% ***band width***
 	- ***ranged Y values*** to show variance only
  	- ***conditional colour*** using Power BI theme sentiment colours (+ve variance=positive; -ve variance=negative)
 	- a ***named style*** 

1c (2) - In-Period Variance Background Rectangle:
- a ***rect*** mark with:
	- ***rounded corners***
 	- 95% ***band width***
    - ***conditional Y offset*** (+ve variance=-16 px; -ve variance=16 px) 
	- same colour as the visual background (white) to ensure clarity when label overlaps Y-axis gridlines
	- a ***named style***

1c (3) - In-Period Variance Label:
- a ***text*** mark with:
    - ***conditional Y offset*** (+ve variance=-10 px; -ve variance=10 px) 
	- ***label formatting*** using a 3-part Power BI format string as enabled by Deneb to display signed values
	- a ***named style***

1c (4) - In-Period Variance % Label:
- a ***text*** mark with:
    - ***conditional Y offset*** (+ve variance=-22 px; -ve variance=22 px) 
	- ***label formatting*** using a 3-part Power BI format string as enabled by Deneb to display signed values
	- a ***named style***

2 - Legend:
- an ***arc*** mark with:
    - a 3-record *hard-coded* dataset
    - a *radius* of zero to leverage *Vega-Lite's automatic legend generation*
    - a *scale/domain/range* block to set the colours (+ve and -ve to the *Power BI theme sentiment colours* [positive, negative])
    - hard-coded ***X*** and ***Y*** positions to place the legend centred below the visual
    	- ***X*** position set to 50% of the visual width minus a constant (120 px)

3 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - line break character string (|) 
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
    - general ***axis*** attributes (domain [enabled], domain colour, ticks [disabled], label font attributes [family, size, colour])
    - ***X*** axis (discrete) attributes (grid [disabled], label attributes [angle align, padding])
    - ***Y*** axis (quantitative) attributes (grid [enabled], grid colour, label padding)  
    - legend label font attributes (family, size, colour)
    - named styles:
        - note vertical leader line attributes (stroke [dashed], colour)
        - note horizontal leader line attributes (stroke width, colour)
        - note background rectangle attributes (corner rounding, stroke colour, fill colour)
        - note variance label font attributes (family, size, weight, style, colour)
        - note variance % label font attributes (family, size, weight, style, colour)
        - out-period bar attributes (corner rounding, stroke colour, fill colour, opacity)
        - out-period value background rectangle attributes (corner rounding, colour)
        - out-period value label font attributes (family, size, weight, style, colour)
        - in-period bar attributes (corner rounding, opacity)
        - in-period variance background rectangle attributes (corner rounding, colour)
        - in-period variance label font attributes (family, size, weight, style, colour)
        - in-period variance % label font attributes (family, size, weight, style, colour) 

<hr>

### Links:

Here's the template:

[913.1 - JSON - Deneb Template - Waterfall Chart with Period Variance](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/912.1%20-%20deneb_template.area_chart_with_min_max_variance.v1.8.2.json) *** FIX *** <br>

<br>

Here's an example Power BI file using the template:

[913.2 - PBIX - Deneb Example - Waterfall Chart with Period Variance](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/912.2%20-%20Deneb%20Reusable%20Components%20-%20Area%20Chart%20with%20Min-Max%20Variance%20-%20V1.8.2.pbix) *** FIX *** <br>

*- eof*
