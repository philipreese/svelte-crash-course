<script lang="ts">
    import * as images from "../image";
    interface Quiz {
        id: number;
        name: String;
        imageUrl: keyof typeof images;
        questions: {
            id: number;
            text: string;
            answer: string;
            options: { id: number; text: string; label: string }[];
        }[];
    }

    export let quiz: Quiz;
</script>

<div
    class="quiz-card shadow w-[250px] rounded overflow-hidden cursor-pointer m-2"
>
    <img src={images[quiz.imageUrl]} alt={quiz.name.toString()} class="h-44" />
    <div class="flex items-center justify-between py-3 px-2">
        <h1 class="font-bold">{quiz.name}</h1>
        <p>
            {quiz.questions.length} question{quiz.questions.length > 1
                ? "s"
                : ""}
        </p>
    </div>
</div>
