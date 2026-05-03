---
theme: dashboard
toc: false
---

# Distribución Espacial de los Apellidos en Puerto Rico

**Fuente:** Centro de Recaudación de Ingresos Municipales (CRIM)

**URL:** https://catastro.crimpr.net/cdprpc/

```js
import * as aq from "npm:arquero";
const op = aq.op;
```

```js
const parquetWasm = await import("https://cdn.jsdelivr.net/npm/parquet-wasm@0.1.1/web.js");
const init = parquetWasm.default;
const readParquet = parquetWasm.readParquet;
await init();
```

```js
const apellidos = await (async () => {
  const file = FileAttachment("apellidos_puertorico_brotli.parquet");
  const arrayBuffer = await file.arrayBuffer();
  const arr = new Uint8Array(arrayBuffer);
  const arrowIPC = readParquet(arr);
  const dt = aq.fromArrow(arrowIPC);
  return dt.objects();
})();
```

```js
const puertoricoGeo = await FileAttachment("puertorico-geo.json").json();
```

```js
const miApellido = view(Inputs.text({label: "Apellido", value: "VEGA", placeholder: "Ej: RIVERA"}));
```

```js
const poblacion = [
  {Municipio: "ADJUNTAS", Poblacion: 17713},
  {Municipio: "AGUADA", Poblacion: 37277},
  {Municipio: "AGUADILLA", Poblacion: 55233},
  {Municipio: "AGUAS BUENAS", Poblacion: 25228},
  {Municipio: "AIBONITO", Poblacion: 23457},
  {Municipio: "AÑASCO", Poblacion: 27368},
  {Municipio: "ARECIBO", Poblacion: 82044},
  {Municipio: "ARROYO", Poblacion: 17318},
  {Municipio: "BARCELONETA", Poblacion: 23432},
  {Municipio: "BARRANQUITAS", Poblacion: 28755},
  {Municipio: "BAYAMÓN", Poblacion: 170694},
  {Municipio: "CABO ROJO", Poblacion: 47077},
  {Municipio: "CAGUAS", Poblacion: 117162},
  {Municipio: "CAMUY", Poblacion: 30504},
  {Municipio: "CANÓVANAS", Poblacion: 43559},
  {Municipio: "CAROLINA", Poblacion: 151183},
  {Municipio: "CATAÑO", Poblacion: 24888},
  {Municipio: "CAYEY", Poblacion: 43638},
  {Municipio: "CEIBA", Poblacion: 11011},
  {Municipio: "CIALES", Poblacion: 16912},
  {Municipio: "CIDRA", Poblacion: 40343},
  {Municipio: "COAMO", Poblacion: 38432},
  {Municipio: "COMERÍO", Poblacion: 19539},
  {Municipio: "COROZAL", Poblacion: 33533},
  {Municipio: "CULEBRA", Poblacion: 1314},
  {Municipio: "DORADO", Poblacion: 37208},
  {Municipio: "FAJARDO", Poblacion: 31743},
  {Municipio: "FLORIDA", Poblacion: 11910},
  {Municipio: "GUÁNICA", Poblacion: 16031},
  {Municipio: "GUAYAMA", Poblacion: 40917},
  {Municipio: "GUAYANILLA", Poblacion: 18714},
  {Municipio: "GUAYNABO", Poblacion: 81960},
  {Municipio: "GURABO", Poblacion: 45986},
  {Municipio: "HATILLO", Poblacion: 38955},
  {Municipio: "HORMIGUEROS", Poblacion: 15898},
  {Municipio: "HUMACAO", Poblacion: 51418},
  {Municipio: "ISABELA", Poblacion: 42420},
  {Municipio: "JAYUYA", Poblacion: 14906},
  {Municipio: "JUANA DÍAZ", Poblacion: 47718},
  {Municipio: "JUNCOS", Poblacion: 38155},
  {Municipio: "LAJAS", Poblacion: 22989},
  {Municipio: "LARES", Poblacion: 25388},
  {Municipio: "LAS MARÍAS", Poblacion: 8599},
  {Municipio: "LAS PIEDRAS", Poblacion: 36459},
  {Municipio: "LOÍZA", Poblacion: 25855},
  {Municipio: "LUQUILLO", Poblacion: 18547},
  {Municipio: "MANATÍ", Poblacion: 39692},
  {Municipio: "MARICAO", Poblacion: 5766},
  {Municipio: "MAUNABO", Poblacion: 10690},
  {Municipio: "MAYAGÜEZ", Poblacion: 71217},
  {Municipio: "MOCA", Poblacion: 36196},
  {Municipio: "MOROVIS", Poblacion: 31461},
  {Municipio: "NAGUABO", Poblacion: 25066},
  {Municipio: "NARANJITO", Poblacion: 28557},
  {Municipio: "OROCOVIS", Poblacion: 20102},
  {Municipio: "PATILLAS", Poblacion: 17334},
  {Municipio: "PEÑUELAS", Poblacion: 21074},
  {Municipio: "PONCE", Poblacion: 131881},
  {Municipio: "QUEBRADILLAS", Poblacion: 24036},
  {Municipio: "RINCÓN", Poblacion: 14088},
  {Municipio: "RÍO GRANDE", Poblacion: 50550},
  {Municipio: "SABANA GRANDE", Poblacion: 22397},
  {Municipio: "SALINAS", Poblacion: 27176},
  {Municipio: "SAN GERMÁN", Poblacion: 32438},
  {Municipio: "SAN JUAN", Poblacion: 318441},
  {Municipio: "SAN LORENZO", Poblacion: 37667},
  {Municipio: "SAN SEBASTIÁN", Poblacion: 36563},
  {Municipio: "SANTA ISABEL", Poblacion: 21720},
  {Municipio: "TOA ALTA", Poblacion: 72033},
  {Municipio: "TOA BAJA", Poblacion: 73405},
  {Municipio: "TRUJILLO ALTO", Poblacion: 65554},
  {Municipio: "UTUADO", Poblacion: 28325},
  {Municipio: "VEGA ALTA", Poblacion: 37406},
  {Municipio: "VEGA BAJA", Poblacion: 52646},
  {Municipio: "VIEQUES", Poblacion: 8249},
  {Municipio: "VILLALBA", Poblacion: 22143},
  {Municipio: "YABUCOA", Poblacion: 33149},
  {Municipio: "YAUCO", Poblacion: 32174}
];
```

```js
const conteoPorMunicipio = Object.entries(
  apellidos
    .filter(d => d.Nombre === miApellido.toUpperCase())
    .reduce((acc, d) => {
      acc[d.Municipio] = (acc[d.Municipio] || 0) + 1;
      return acc;
    }, {})
).map(([Municipio, Conteo]) => ({Municipio, Conteo}))
 .sort((a, b) => b.Conteo - a.Conteo);
```

```js
const frecuenciaNormalizada = conteoPorMunicipio.map(d => {
  const mun = poblacion.find(p => p.Municipio === d.Municipio);
  const pob = mun ? mun.Poblacion : 1;
  return {
    Municipio: d.Municipio,
    Conteo: d.Conteo,
    FrecuenciaNormalizada: d.Conteo / pob
  };
}).sort((a, b) => b.FrecuenciaNormalizada - a.FrecuenciaNormalizada);
```

```js
const totalApellido = conteoPorMunicipio.reduce((acc, d) => acc + d.Conteo, 0);
const topMunicipio = frecuenciaNormalizada[0];
```

<div class="grid grid-cols-3">
  <div class="card">
    <h2>Apellido: <span style="color:#e63946;">${miApellido.toUpperCase()}</span></h2>
  </div>
  <div class="card">
    <h3>Municipio más frecuente:</h3>
    <h2 style="color:#e63946;">${topMunicipio ? topMunicipio.Municipio : "N/A"}</h2>
    <p>${topMunicipio ? (topMunicipio.FrecuenciaNormalizada * 100).toFixed(2) + "% de la población" : ""}</p>
  </div>
  <div class="card">
    <h3>Total de registros:</h3>
    <h2 style="color:#e63946;">${totalApellido.toLocaleString()}</h2>
  </div>
</div>

<div class="grid grid-cols-1">
  <div class="card">${resize((width) => Plot.plot({
    title: `Frecuencia Normalizada de ${miApellido.toUpperCase()} por Municipio`,
    width,
    height: 500,
    marginLeft: 150,
    marginBottom: 60,
    x: { label: "FRECUENCIA NORMALIZADA", grid: true },
    y: { label: "Municipios" },
    color: { range: ["#fde0d0", "#8b0000"] },
    marks: [
      Plot.barX(frecuenciaNormalizada.slice(0, 10), {
        x: "FrecuenciaNormalizada",
        y: "Municipio",
        sort: { y: "-x" },
        fill: "FrecuenciaNormalizada"
      })
    ]
  }))}</div>
</div>

```js
const coroMap = (() => {
  const conteo = new Map(frecuenciaNormalizada.map(d => [d.Municipio, d.FrecuenciaNormalizada]));
  return Plot.plot({
    title: `Mapa Coroplético - ${miApellido.toUpperCase()}`,
    width,
    height: 500,
    projection: {type: "mercator", domain: puertoricoGeo.pueblos},
    style: {background: "black"},
    color: { scheme: "OrRd", unknown: "#222" },
    marks: [
      Plot.geo(puertoricoGeo.pueblos, {
        fill: d => conteo.get(d.properties.NAME.toUpperCase()) ?? 0,
        stroke: "white",
        strokeWidth: 0.5,
        title: d => d.properties.NAME,
        tip: true
      })
    ]
  });
})();
```

<div class="grid grid-cols-2">
  <div class="card">${coroMap}</div>
  <div class="card">${resize((width) => Plot.plot({
    title: `Mapa de Puntos - ${miApellido.toUpperCase()}`,
    width,
    height: 500,
    projection: {type: "mercator", domain: puertoricoGeo.pueblos},
    style: {background: "black"},
    marks: [
      Plot.geo(puertoricoGeo.pueblos, {
        fill: "#222",
        stroke: "white",
        strokeWidth: 0.5
      }),
      Plot.dot(
        apellidos.filter(d => d.Nombre === miApellido.toUpperCase()),
        {
          x: "Longitude",
          y: "Latitude",
          fill: "red",
          opacity: 0.3,
          r: 2
        }
      )
    ]
  }))}</div>
</div>

<div class="grid grid-cols-1">
  <div class="card">
    <h3>Ranking de Municipios - ${miApellido.toUpperCase()}</h3>

```js
Inputs.table(frecuenciaNormalizada, {
  columns: ["Municipio", "Conteo", "FrecuenciaNormalizada"],
  header: {
    Municipio: "Municipio",
    Conteo: "Total Registros",
    FrecuenciaNormalizada: "Frecuencia Normalizada"
  },
  format: {
    FrecuenciaNormalizada: d => (d * 100).toFixed(2) + "%"
  },
  sort: "FrecuenciaNormalizada",
  reverse: true
})
```

  </div>
</div>