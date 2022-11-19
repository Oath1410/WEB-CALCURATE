<script>
  import { now } from "svelte/internal";

  // bypass
  // let data = { oat: 20, nut: 200, ing: 1000 };

  let num;

  let show = true;

  let data = {};

  let log = {};

  let money = 0;

  let list = [];

  function create() {
    for (let i = 1; i <= num; i++) {
      let name = prompt("ใส่ชื่อคนที่" + i);

      while (name == "") {
        name = prompt("ใส่ชื่อคนที่" + i);
      }

      data[name] = 0;
      log[name] = [];

      list.push("");

      show = false;
      document.getElementById("section").style.display = "none";
      document.getElementById("section2").style.display = "block";
    }
  }

  function add(name) {
    // @ts-ignore
    let amount = document.getElementById(name).value;
    if (amount == "" || amount == 0 || amount == null) {
      amount = 0;
    }
    data[name] = data[name] + parseInt(amount);
    if (amount != 0) {
      log[name].push(amount);
    }
    // ปรับค่าเป็น 0 หลังจากบันทึก

    // @ts-ignore
    document.getElementById(name).value = "";

    for (let i = 0; i < list.length; i++) {
      list[i] = "";
    }
  }

  function buttonadd(i, amount) {
    // @ts-ignore
    list[i] = +list[i] + amount;
  }
</script>

<main>
  <section id="section" class="vh-100" style="background-color: #508bfc;">
    <div class="container py-5 h-100 ">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card shadow-2-strong" style="border-radius: 1rem;">
            <div class="card-body p-5 text-center">
              <h1 class="text-primary mb-4">คำนวณเงินไพ่</h1>
              {#if show}
                <div class="form-outline mb-4">
                  <input
                    class="form-control form-control-lg"
                    bind:value={num}
                    type="number"
                    on:click={() => create()}
                    on:keypress={(e) => {
                      if (e.key == "Enter") {
                        create();
                      }
                    }}
                    placeholder="จำนวนผู้เล่น"
                  />
                </div>
                <button
                  type="button"
                  class="btn btn-primary btn-lg btn-block"
                  on:click={() => create()}
                >
                  ยืนยัน</button
                >
              {/if}
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section
    id="section2"
    class="vh-100"
    style="background-color: #508bfc; display:none;"
  >
    <div class="container py-5 h-100 ">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card shadow-2-strong" style="border-radius: 1rem;">
            <div class="card-body p-5 text-center">
              {#each Object.keys(data) as name, i}
                <div class="d-flex justify-content-center align-items-center">
                  {#if name == "null"}
                    <h2 id="name" class="">มึงไม่กรอกชื่อละไอ้สัส ไปรีเว็ป</h2>
                  {:else}
                    <h2 id="name" class="">{name}</h2>
                  {/if}
                  <h2>(</h2>
                  <h2 id="money" class="text-danger">{data[name]}</h2>
                  <h2>)</h2>
                </div>
                <!-- ปุ่มคิดเงิน-->
                <div class="input-group mb-3">
                  <input
                    class="form-control form-control-lg"
                    type="number"
                    id={name}
                    bind:value={list[i]}
                    placeholder="ใส่จำนวนเงิน"
                  />
                  <button
                    class="btn btn-primary btn-lg btn-block"
                    on:click={() => add(name)}>คิดเงิน</button
                  >
                </div>

                <div
                  class="btn-group pb-2"
                  role="group"
                  aria-label="Basic example"
                >
                  <button
                    class="btn btn-success"
                    type="button"
                    on:click={() => buttonadd(i, 5)}>+5</button
                  >
                  <button
                    class="btn btn-success"
                    on:click={() => buttonadd(i, 10)}>+10</button
                  >
                  <button
                    class="btn btn-success"
                    on:click={() => buttonadd(i, 20)}>+20</button
                  >
                  <button
                    class="btn btn-success"
                    on:click={() => buttonadd(i, 50)}>+50</button
                  >
                  <button
                    class="btn btn-success"
                    on:click={() => buttonadd(i, 100)}
                  >
                    +100</button
                  >
                </div>

                <div
                  class="btn-group pb-2"
                  role="group"
                  aria-label="Basic example"
                >
                  <button
                    class="btn btn-danger"
                    on:click={() => buttonadd(i, -5)}>-5</button
                  >
                  <button
                    class="btn btn-danger"
                    on:click={() => buttonadd(i, -10)}>-10</button
                  >
                  <button
                    class="btn btn-danger"
                    on:click={() => buttonadd(i, -20)}>-20</button
                  >
                  <button
                    class="btn btn-danger"
                    on:click={() => buttonadd(i, -50)}>-50</button
                  >
                  <button
                    class="btn btn-danger"
                    on:click={() => buttonadd(i, -100)}>-100</button
                  >
                </div>

                {#if log[name].length < 5}
                  <p>{log[name]}</p>
                {:else}
                  <p>{log[name].slice(-5)}</p>
                {/if}

                <hr class="my-4" />
              {/each}
              <p class="text-danger fs-1">ใช้เว็บนี้แล้วรวย</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Kanit&display=swap");
  * {
    font-family: "Kanit", sans-serif;
  }

  #name {
    color: darkblue;
  }

  h2 {
    padding: 0 3px;
    font-size: 40px;
  }
</style>
