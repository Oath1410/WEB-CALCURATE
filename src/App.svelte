<script>
  let num;

  let show = true;

  let data = {};

  function create() {
    for (let i = 1; i <= num; i++) {
      let name = prompt("ใส่ชื่อคนที่" + i);
      data[name] = 0;
      show = false;
    }
  }

  function add(name) {
    // @ts-ignore
    let amount = document.getElementById(name).value;
    data[name] = data[name] + parseInt(amount);

    // ปรับค่าเป็น 0 หลังจากบันทึก

    // @ts-ignore
    document.getElementById(name).value = "";
  }
</script>

<main>
  <!-- bootstrap 5 -->

  <div class="header">
    <h1>คำนวณเงินไพ่</h1>
    {#if show}
      <input bind:value={num} type="number" placeholder="จำนวนผู้เล่น" />
      <button
        class="button-9"
        on:click={() => create()}
        on:keypress={(e) => {
          if (e.key == "Enter") {
            create();
          }
        }}>ยืนยัน</button
      >
    {/if}
  </div>
  <div>
    {#each Object.keys(data) as name}
      <div class="list">
        <h2>{name}</h2>

        <h2 class="money">( {data[name]} )</h2>

        <!-- ปุ่มคิดเงิน-->
        <input
          type="number"
          id={name}
          value="money"
          placeholder="ใส่จำนวนเงิน"
        />
        <button class="button-3" on:click={() => add(name)}>ยืนยัน</button>
        <br />
        <br />
        <button class="button-3" on:click={() => (data[name] += 5)}>+5</button>
        <button class="button-3" on:click={() => (data[name] += 10)}>+10</button
        >
        <button class="button-3" on:click={() => (data[name] += 20)}>+20</button
        >
        <button class="button-3" on:click={() => (data[name] += 50)}>+50</button
        >
        <button class="button-3" on:click={() => (data[name] += 100)}
          > +100</button
        >
        <br />
        <br />
        <button class="button-3" on:click={() => (data[name] -= 5)}>-5</button>
        <button class="button-3" on:click={() => (data[name] -= 10)}>-10</button
        >
        <button class="button-3" on:click={() => (data[name] -= 20)}>-20</button
        >
        <button class="button-3" on:click={() => (data[name] -= 50)}>-50</button
        >
        <button class="button-3" on:click={() => (data[name] -= 100)}
          >-100</button
        >
        <br />
        <br />
      </div>
    {/each}
  </div>
</main>

<style>
  .list {
    align-items: center;
  }

  h2 {
    color: rgb(0, 0, 0);
    font-size: 30px;
    font-weight: 600;
    text-align: center;
    margin: 0;
  }

  .money {
    color: #ff0000;
    font-size: 35px;
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

  input {
    width: 50%;
    padding: 10px 15px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 2px solid red;
    border-radius: 4px;
    background-color: #ffffff;
    
    font-size: 20px;
    
  }
  .header {
    padding: 60px;
    text-align: center;
    background: #1abc9c;
    color: white;
    font-size: 20px;
  }

  input[type="number"] {
    color: rgb(0, 0, 0);
  }

  .button-9 {
    appearance: button;
    backface-visibility: hidden;
    background-color: #405cf5;
    border-radius: 6px;
    border-width: 0;
    box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
      rgba(50, 50, 93, 0.1) 0 2px 5px 0, rgba(0, 0, 0, 0.07) 0 1px 1px 0;
    box-sizing: border-box;
    color: #fff;
    cursor: pointer;
    font-family: -apple-system, system-ui, "Segoe UI", Roboto, "Helvetica Neue",
      Ubuntu, sans-serif;
    font-size: 100%;
    height: 44px;
    line-height: 1.15;
    margin: 12px 0 0;
    outline: none;
    overflow: hidden;
    padding: 0 25px;
    position: relative;
    text-align: center;
    text-transform: none;
    transform: translateZ(0);
    transition: all 0.2s, box-shadow 0.08s ease-in;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
    width: 100%;
  }

  .button-9:disabled {
    cursor: default;
  }

  .button-9:focus {
    box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
      rgba(50, 50, 93, 0.2) 0 6px 15px 0, rgba(0, 0, 0, 0.1) 0 2px 2px 0,
      rgba(50, 151, 211, 0.3) 0 0 0 4px;
  }

  .button-3 {
    appearance: none;
    background-color: #2ea44f;
    border: 1px solid rgba(27, 31, 35, 0.15);
    border-radius: 6px;
    box-shadow: rgba(27, 31, 35, 0.1) 0 1px 0;
    box-sizing: border-box;
    color: #fff;
    cursor: pointer;
    display: inline-block;
    font-family: -apple-system, system-ui, "Segoe UI", Helvetica, Arial,
      sans-serif, "Apple Color Emoji", "Segoe UI Emoji";
    font-size: 14px;
    font-weight: 600;
    line-height: 20px;
    padding: 6px 16px;
    position: relative;
    text-align: center;
    text-decoration: none;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
    vertical-align: middle;
    white-space: nowrap;
  }

  .button-3:focus:not(:focus-visible):not(.focus-visible) {
    box-shadow: none;
    outline: none;
  }

  .button-3:hover {
    background-color: #2c974b;
  }

  .button-3:focus {
    box-shadow: rgba(46, 164, 79, 0.4) 0 0 0 3px;
    outline: none;
  }

  .button-3:disabled {
    background-color: #94d3a2;
    border-color: rgba(27, 31, 35, 0.1);
    color: rgba(255, 255, 255, 0.8);
    cursor: default;
  }

  .button-3:active {
    background-color: #298e46;
    box-shadow: rgba(20, 70, 32, 0.2) 0 1px 0 inset;
  }
</style>
