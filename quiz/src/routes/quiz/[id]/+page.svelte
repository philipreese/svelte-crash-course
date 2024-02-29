<script lang="ts">
    import QuestionOption from "./components/QuestionOption.svelte";
    import QuestionText from "./components/QuestionText.svelte";

    export let data: any;

    let currentQuestionIndex = 0;
    $: question = data.questions[currentQuestionIndex];
</script>

<div class="w-full">
    <QuestionText text={question.question} />
    <div class="flex justify-between flex-wrap cursor-pointer">
        {#each question.options as option (option.id)}
            <QuestionOption {option} />
        {/each}
    </div>
</div>
