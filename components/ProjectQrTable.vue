<template>
  <table class="project-qr-table">
    <colgroup>
      <col class="project-column" />
      <col class="purpose-column" />
      <col class="qr-column" />
    </colgroup>
    <thead>
      <tr>
        <th>Crate</th>
        <th>What it does</th>
        <th>Scan</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="project-name">metrique</span></td>
        <td>Wide-event metrics for production services</td>
        <td>
          <img src="/images/qr-metrique.svg" alt="QR code for metrique" />
        </td>
      </tr>
      <tr>
        <td><span class="project-name">dial9</span></td>
        <td>Always-on runtime traces and profiling</td>
        <td>
          <img src="/images/qr-dial9.svg" alt="QR code for dial9" />
        </td>
      </tr>
      <tr>
        <td><span class="project-name">Shuttle</span></td>
        <td>Explores concurrent thread schedules</td>
        <td>
          <img src="/images/qr-shuttle.svg" alt="QR code for Shuttle" />
        </td>
      </tr>
      <tr>
        <td><span class="project-name">Turmoil</span></td>
        <td>Simulates hosts and network failures</td>
        <td>
          <img src="/images/qr-turmoil.svg" alt="QR code for Turmoil" />
        </td>
      </tr>
      <tr>
        <td><span class="project-name">Hydro</span></td>
        <td>Builds and tests distributed Rust programs</td>
        <td>
          <img src="/images/qr-hydro.svg" alt="QR code for Hydro" />
        </td>
      </tr>
      <tr>
        <td><span class="project-name">Battery Packs</span></td>
        <td>Shares curated crate sets for a domain</td>
        <td>
          <img src="/images/qr-battery-pack.svg" alt="QR code for Battery Packs" />
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
:global(.slidev-layout.project-table-slide) {
  padding-bottom: 1.6rem;
  padding-top: 1.6rem;
}

.project-qr-table {
  border-collapse: collapse;
  height: 100%;
  table-layout: fixed;
  width: 100%;
}

.project-column {
  width: 25%;
}

.purpose-column {
  width: 57%;
}

.qr-column {
  width: 18%;
}

.project-qr-table th {
  border-bottom: 2px solid var(--ink);
  color: var(--rust);
  font-size: 0.72rem;
  font-weight: 780;
  padding: 0.25rem 0.8rem 0.5rem;
  text-align: left;
  text-transform: uppercase;
}

.project-qr-table th:last-child,
.project-qr-table td:last-child {
  text-align: center;
}

.project-qr-table td {
  border-bottom: 1px solid var(--line);
  color: var(--muted);
  font-size: 1rem;
  line-height: 1.2;
  padding: 0.28rem 0.8rem;
  vertical-align: middle;
}

.project-qr-table tbody tr:last-child td {
  border-bottom: 0;
}

.project-name {
  color: var(--ink);
  font-size: 1.22rem;
  font-weight: 760;
}

.project-qr-table img {
  display: inline-block;
  height: 3.55rem;
  width: 3.55rem;
}
</style>
