<script lang="ts">
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Label } from "$lib/components/ui/label/index.js";

  $: frontLeft = 0.0;
  $: frontRight = 0.0; 
  $: backLeft = 0.0;
  $: backRight = 0.0;
  $: averageValue = 0.0;

  $: displacementDraftTop = 0.0;
  $: displacementDraftBottom = 0.0;
  $: deadweightTop = 0.0;
  $: deadweightBottom = 0.0;

  $: deadweightValue = 0.0;

  const onAverageClick = () => {
    let sum = Number(frontLeft) + Number(frontRight) + Number(backRight) + Number(backLeft)
    let average = sum / 4.00
    averageValue = average
  }

  const onInterpolate = () => {
    let diffWithAverage = Number(averageValue) - Number(displacementDraftBottom);
    console.log("diffWithAverage", diffWithAverage)

    let diffWithDisplacementTop = Number(displacementDraftTop) - Number(displacementDraftBottom);
    console.log("diffWithDisplacementTop", diffWithDisplacementTop)

    let diffDeadweightTopBottom = Number(deadweightTop) - Number(deadweightBottom);
    console.log("diffDeadweightTopBottom", diffDeadweightTopBottom)

    let diffDeadweightAverage = (diffWithAverage * diffDeadweightTopBottom) / diffWithDisplacementTop;
    console.log("diffDeadweightAverage", diffDeadweightAverage)

    let averageDeadweight = Number(deadweightBottom) + diffDeadweightAverage;
    console.log(averageDeadweight)

    deadweightValue = averageDeadweight;
  }
</script>
 
<div>
  <h1 class="text-white font-bold text-2xl text-center">
    Perhitungan Draft Tongkang
  </h1>
  
  <div class="grid grid-cols-2 grid-rows-2 gap-3 mt-3">
    <div>
      <Label class="text-white" for="frontLeft">Depan Kiri</Label>
      <Input id="frontLeft" type="number" placeholder="Depan Kiri" class="max-w-xs my-1" bind:value={frontLeft}/>
    </div>
    <div>
      <Label class="text-white" for="frontRight">Depan Kanan</Label>
      <Input id="frontRight" type="number" placeholder="Depan Kanan" class="max-w-xs my-1" bind:value={frontRight}/>
    </div>
    <div>
      <Label class="text-white" for="backLeft">Belakang Kiri</Label>
      <Input id="backLeft" type="number" placeholder="Belakang Kiri" class="max-w-xs my-1" bind:value={backLeft}/>
    </div>
    <div>
      <Label class="text-white" for="backRight">Belakang Kanan</Label>
      <Input id="backRight" type="number" placeholder="Belakang Kanan" class="max-w-xs my-1" bind:value={backRight}/>
    </div>
  </div>
  
  <Button variant="outline" class="w-full mt-5" on:click={onAverageClick}>Hitung Rata-Rata</Button>

  <div class="mt-3">
    <Label class="text-white" for="averageDraft">Nilai Rata-Rata Draft</Label>
    <Input id="averageDraft" type="number" disabled placeholder="Hasil Rata Rata" class="w-full my-1" bind:value={averageValue}/>
  </div>

  
  <h1 class="text-white font-bold text-xl text-center my-5">
    Tabel Displacement
  </h1>
  
  <div class="grid grid-cols-2 grid-rows-2 gap-3">
    <div>  
      <Label class="text-white" for="displacementDraftBottom">Draft Bawah</Label>
      <Input id="displacementDraftBottom" type="number" placeholder="Draft Bawah" class="max-w-xs my-1 mx-1" bind:value={displacementDraftBottom}/>
    </div>
    <div>
      <Label class="text-white" for="deadweightBottom">Deadweight Bawah</Label>
      <Input id="deadweightBottom" type="number" placeholder="Deadweight Bawah" class="max-w-xs my-1 mx-1" bind:value={deadweightBottom}/>
    </div>
    <div>
      <Label class="text-white" for="displacementDraftTop">Draft Atas</Label>
      <Input type="number" placeholder="Draft Atas" class="max-w-xs my-1 mx-1" bind:value={displacementDraftTop}/>
    </div>
    <div>
      <Label class="text-white" for="deadweightTop">Deadweight Atas</Label>
      <Input type="number" placeholder="Deadweight Atas" class="max-w-xs my-1 mx-1" bind:value={deadweightTop}/>
    </div>
  </div>
 
  
  <Button variant="outline" class="w-full mt-5" on:click={onInterpolate}>Interpolate</Button>

  <div class="mt-3">
    <Label for="averageDeadweight" class="text-white">Hasil Perhitungan Draft</Label>
    <Input id="averageDeadweight" type="number" disabled placeholder="Hasil Rata Rata" class="w-full my-3" bind:value={deadweightValue}/>
  </div>
</div>
