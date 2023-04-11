# React-Image-Fetcher-
Finding The React Image usiing JS
import React, { useState } from "react";
import Loader from "./Loader";

function PhotoFrame({ url, title }) {
  return (
    <div className="photoframe">
      <img src={url} alt={title} />
      <div className="caption">{title}</div>
    </div>
  );
}

function PhotoApp() {
  const [photo, setPhoto] = useState(null);

  function handleInputChange(event) {
    const id = event.target.value;
    fetch(`https://jsonplaceholder.typicode.com/photos/${id}`)
      .then((response) => response.json())
      .then((data) => setPhoto(data))
      .catch((error) => console.log(error));
  }

  return (
    <div>
      <input type="number" onChange={handleInputChange} />
      {photo ? (
        <PhotoFrame url={photo.url} title={photo.title} />
      ) : (
        <Loader />
      )}
    </div>
  );
}

export default PhotoApp;

