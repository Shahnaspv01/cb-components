<svelte:options tag="cb-navbar" />

<script>
  import ClassroomCourses from './classroom-courses.svelte'
  import OnlineCourses from './online-courses.svelte'

  // by default use latest motley version for unpkg
  export let topalign = "center"
  export let expanded = false
  export let tab = "classroom"
  export let css = "https://unpkg.com/@coding-blocks/motley/dist/app.min.css"

  let topStyle = 'justify-content-center'
  let icon = faChevronUp

  $: switch (topalign) {
    case 'left': topStyle = 'justify-content-start'; break;
    case 'right': topStyle = 'justify-content-end'; break;
    default: topStyle = 'justify-content-center'
  }

  const toggleExpanded = () => expanded = !expanded

</script>

<style>
    a:hover {
      text-decoration: underline;
    }

    .hover-grey.selected:hover {
      background: unset;
    }

    .a-hb {
      display: none;
    }
    
</style>

<link rel="stylesheet" href={css} />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.9.0/css/all.min.css" integrity="sha256-UzFD2WYH2U1dQpKDjjZK72VtPeWP50NoJjd26rnAdUI=" crossorigin="anonymous" />
<link href="https://fonts.googleapis.com/css?family=Nunito+Sans:400,600,700,800" rel="stylesheet">
<link href="https://minio.codingblocks.com/hackerblocks-images/Gilroy.ttf" rel="stylesheet">


<div class="a-hb d-md-block d-none">

  <div class="border">
    <div class="d-flex {topStyle} py-3 pr-5">
      <span class="px-3 pointer" on:click={toggleExpanded}>
        Courses
        <i class="ml-1 fas fa-chevron-{expanded ? 'up' : 'down'}"></i>

      </span>
      <div class="px-3">
        <a href="#">Products</a>
      </div>
      <div class="px-3">
        <a href="https://codingblocks.com/about.html">About Us</a>
      </div>
      <div class="px-3">
        <a href="https://codingblocks.com/resources">Resources</a>
      </div>
      <div class="px-3">
        <a href="https://codingblocks.com/campus-ambassador-program.html">Campus Ambassadors</a>
      </div>
      <div class="px-3">
        <a href="https://codingblocks.com/centres/">Contact Us</a>
      </div>
      <slot name="header"></slot>
    </div>

  </div>

  {#if expanded}
    <div class="row no-gutters cb-navbar-expanded" style="overflow: hidden">
      <div class="cb-navbar-side col-3">
        <div class="py-5 font-md bold hover-grey">
          <div class="font-lg my-4 offset-3">Our Courses</div>
        </div>
        <div class="py-4 font-md bold hover-grey {tab == 'classroom' && 'selected'}" on:click={() => tab = "classroom"}>
          <div class="offset-3">
            <div>Classroom Courses</div>
            <a href="https://codingblocks.com/classroom-courses/" class="font-mds orange"> 
              Explore all 
            </a>
          </div>
        </div>
        <div class="py-4 font-md bold hover-grey {tab == 'online' && 'selected'}"  on:click={() => tab = "online"}>
          <div class="offset-3">
            <div>Online Courses</div>
            <a href="https://online.codingblocks.com/courses" class="font-mds orange"> 
              Explore all 
            </a>
          </div>
        </div>
        
      </div>
      <div class="col-9 font-mds">
        {#if tab=="classroom"}
          <ClassroomCourses />
        {:else}
          <OnlineCourses />
        {/if}
      </div>
    </div>
  {/if}
</div>