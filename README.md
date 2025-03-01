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
