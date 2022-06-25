<script>

    let subjects = [{
        id: 1,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },{
        id: 2,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },{
        id: 3,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },{
        id: 4,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },{
        id: 5,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },{
        id: 6,
        grade: 'A+',
        name: 'CS',
        credits: 3,
    },
    ];
    const convert= {
        'A+':4.0,
        'A':3.75,
        'B+':3.4,
        'B':3.0,
        'C+':2.5,
        'C':2.0,
        'D':1.0,
        'F':0.0
    }
    subjects.map(subject => {
        subject.gpa=convert[subject.grade];
    });
    let totalGpa=0;
    $: totalGpa = subjects.reduce((accumulator, object) => {
        return accumulator + parseFloat(object.gpa) * parseFloat(object.credits);
    }, 0);
    let totalCredits=0;
    $: totalCredits = subjects.reduce((accumulator, object) => {
        return accumulator + parseFloat(object.credits);
    }, 0);
    $: CurrGpa =   Math.round((totalGpa/totalCredits)*100)/100 ;
    let prevGpa=3.93;
    let prevHours=55;
    let CummulativeGpa;
    $:  CummulativeGpa = Math.round(((prevGpa*prevHours)+CurrGpa*totalCredits)/(prevHours+totalCredits)*100)/100;
    function calculateGpa(){
        let gpa = totalGpa/prevHours;
        let gpaRound = Math.round(gpa*100)/100;
        }
    function add() {
        subjects= subjects.concat({
            id: subjects.length+1,
            grade: 'A+',
            name: 'CS',
            credits: 3,
            gpa: 4.0,
        });
    }
    const remove = (subject) => {
        subjects = subjects.filter((value) => value.id !== subject.id);
        }

</script>
<div class="grid justify-center align-middle ">
    <h1 class="text-4xl text-center pb-4">FCIH GPA Calculator </h1>
    <div class="card bg-base-300">
        <div class="card-body pt-3">
            <p>Previous GPA</p>
            <input class="input " type="number" bind:value="{prevGpa}">
            <p class="pt-2">Total Hours</p>
            <input class="input " type="number" bind:value={prevHours}>
        </div>
    </div>
</div>
<div class="grid text-center pt-3">
    <p>Current Term GPA : {CurrGpa? CurrGpa : 0}</p>
    <p>Cumulative GPA : {CummulativeGpa? CummulativeGpa : 0}</p>
    <p>Hours : {(totalCredits+prevHours)? totalCredits+prevHours : 0}    </p>
</div>
<div class="flex justify-center flex-wrap m-2 ">
    {#each subjects as subject}
        <div class="card max-w-xs  m-2 ">
            <div class="card-body bg-base-300 ">
                <div class="flex justify-center my-3">
                <select  class=" text-2xl  input font-bold text-center w-1/2 mx-auto" title="grade" bind:value={subject.gpa}>
                    {#each Object.entries(convert).map(([key, value]) => ({[key]: value})) as object}
                        <option value="{Object.values(object)}">{Object.keys(object)}</option>
                    {/each}
                </select>
                <input id="ds" type="number" min="2" max="6" class="text-2xl input  font-bold text-center w-1/3 mx-auto" bind:value="{subject.credits}">
                </div>
                <hr>
                <p >Subject GPA: {subject.gpa} </p>
                <p class="flex w-full " >Hours: {subject.credits? subject.credits : 0} <button on:click={() => {remove(subject)}} class=" btn ml-[8.7rem] border-2 border-error bg-transparent text-error text-2xl">X</button></p>
                <div class="flex justify-end"></div>
            </div>
        </div>
    {/each}

</div>

<div class="flex justify-evenly">
<button class=" bg-gray-500   text-3xl btn " on:click={add}>+</button>
</div>


