<script context="module">
    export async function load() {
        const posts = import.meta.globEager('./*.md');
        const postsList = Object.values(posts);
        const postsMeta = postsList.map(post => post.metadata);
        const sortedPosts = postsMeta.sort((a, b) => new Date(b.date) - new Date(a.date));
        return {
            props: {
                posts: sortedPosts
            }
        };
    }
</script>

<script>
    import PostPreview from '$lib/PostPreview.svelte';

    export let posts;
</script>


{#each posts as post}
    <PostPreview post={post} />
{/each}


