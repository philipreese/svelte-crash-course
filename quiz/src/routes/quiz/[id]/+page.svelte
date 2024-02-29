<script lang="ts">
    import QuestionButton from "./components/QuestionButton.svelte";
    import QuestionOption from "./components/QuestionOption.svelte";
    import QuestionText from "./components/QuestionText.svelte";
    import { answers, type Answer } from "../../../store";

    export let data: any;

    let currentQuestionIndex = 0;
    let answersValue: Answer[];
    let selectedOption: null | string = null;
    let showCorrectAnswer: boolean;

    const handleChangeOption = (label: string) => {
        selectedOption = label;
    };

    const handleSubmit = () => {
        if (!selectedOption) return;

        showCorrectAnswer = true;
        answers.update((currentState) => {
            const updatedAnswerState = currentState;
            updatedAnswerState[currentQuestionIndex].isCorrect =
                selectedOption === question.answer;
            return updatedAnswerState;
        });
    };

    answers.subscribe((value) => {
        answersValue = value;
    });

    $: question = data.questions[currentQuestionIndex];
</script>

<div class="w-full">
    <QuestionText text={question.question} />
    <div class="flex justify-between flex-wrap cursor-pointer">
        {#each question.options as option (option.id)}
            <QuestionOption
                {option}
                {selectedOption}
                {handleChangeOption}
                {showCorrectAnswer}
                answer={question.answer}
            />
        {/each}
    </div>
    <QuestionButton {handleSubmit} />
</div>
