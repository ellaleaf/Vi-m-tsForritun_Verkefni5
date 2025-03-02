# Verkefni 5 - Gabríela Líf - Viðmótsforritun

## Tækniskólinn - 2025 - FORR3FV05EU


### Hugmyndin
ég vildi geta notað hendina mína til þess að interacta við hluti í xr.

### Framkvæmd
til að byrja með googlaði ég um dæmi um þetta og það eina sem ég fann var [þetta](https://tympanus.net/codrops/2024/10/24/creating-a-3d-hand-controller-using-a-webcam-with-mediapipe-and-three-js/). En ég skyldi ekki kóðan plús þetta var ekki einmitt það sem ég vildi gera, en ég notaði þetta sem grunn til að byrja.

**[Skref 1](https://github.com/ellaleaf/Vi-m-tsForritun_Verkefni5/blob/c63aa6010c8dbb7745b92087938f28eccda0ce99/docs/skref_1.html)** ég byrja á því að fá media pipe til að virka en þar sem ég sýni hendina í 3d space nota ég ekki canvas.
næst bý ég til basic three.js senu. til þess að sjá hendina bý ég til function sem býr til kúlur fyrir hvert landmark í mediapipe gesturerecognizer.
```javascript
function CreateHand() {
    const sphereMat = new THREE.MeshNormalMaterial();

    const sphereGeo = new THREE.SphereGeometry(0.1, 8, 4);
    const sphereMesh = new THREE.Mesh(sphereGeo, sphereMat);

      for (let i = 0; i < 21; i++) {
        const sphereMeshClone = sphereMesh.clone();
        handsObj.add(sphereMeshClone);
      }
}
```

eftir að instantiate-a function-ið í three.js senuna er sett for loop í animation/render function-ið þar sem hver kúla er gefið sömu hnit og landmark resultin.

```javascript
for (let l = 0; l < 21; l++) {
  console.log(handsObj);
  handsObj.children[l].position.x = - results.landmarks[0][l].x + 0.5;
  handsObj.children[l].position.y = - results.landmarks[0][l].y + 0.8;
  handsObj.children[l].position.multiplyScalar(4);
  handsObj.children[l].position.z = - depthZ;
  
}
```
til þess að fá depthZ sem er z-hnit handarinnar tekur maður tvo landmark punkta, ég notaði punkta 0 og 9, síðan er reiknað lengd á milli punktana sem er breytt í notanleg hnit.

```javascript
const pointA = results.landmarks[0][9];
const pointB = results.landmarks[0][0];

const pointDistance = CalculateDistance(pointA.x, pointA.y, pointB.x, pointB.y )

const depthZ = THREE.MathUtils.mapLinear(pointDistance, 0, 1, -3, 5);
```

eftir þetta fékk ég fullnægjandi [niðurstöður](https://ellaleaf.github.io/Vi-m-tsForritun_Verkefni5/skref_1.html)

**[Skref 2](https://github.com/ellaleaf/Vi-m-tsForritun_Verkefni5/blob/1941554a79ea5393b2d5b5eea7330ecfea7c7df3/docs/skref_2.html)** næst vildi ég geta interact-að við heiminn.
ég byrjaði á því að nota raycasting og nota bara eitt af lanmarkanum í hendinni, en það varð ruglandi svo ég ákvað að sleppa hendinni og nota bara eina kúlu. til þess að gera það minkaði ég hversu margar kúlur voru búnar til í CreateHand() og tók út for loopið. ég notaði gesture recognizer til að vita hvenær notandi lokaði hnefanum sínum á meðan kúlan snerti kubbinn.

þegar að ég reyndi að nota raycaster fyrst var það bæði hægt og buggy, en ég fann [þennan kóða](https://stackoverflow.com/questions/11473755/how-to-detect-collision-in-three-js) sem virkaði betur en það sem ég notaði áður en var enþá hægt.

eftir að gera allt þetta var ekki mikill tími eftir svo ég ákvað að [þetta](https://ellaleaf.github.io/Vi-m-tsForritun_Verkefni5/skref_2.html) var nógu gott

**[Loka Skref](https://github.com/ellaleaf/Vi-m-tsForritun_Verkefni5/blob/11d7d952c8f707c8eba2745cae4c99e65626c64c/docs/lokaverkefni.html)** á meða ég var að gera skref 2 var ég farin að spá í hvort það var ástæða fyrir því að ég var að nota fremri myndavélina og afhverju ég reyndi aldrei að nota bakmyndavél eftir skref 1, en núna átti ég lítin tíma eftir og ég var komin með allt sem ég þurfti.

ég notaði verkefnið sem ég gerði í xr fyrir grunn og setti skref 1 inn í það, sem virkaði en það var mjög hægt. hér er [niðurstaðan](https://ellaleaf.github.io/Vi-m-tsForritun_Verkefni5/lokaverkefni.html).

## Útkoma
https://ellaleaf.github.io/Vi-m-tsForritun_Verkefni5/

því miður gat ég ekki gert einmitt það sem ég vildi vegna tímaskorts og annara takmarka. en annars held ég að þetta er fínt.
